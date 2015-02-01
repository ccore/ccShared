import fnmatch
import os

def scanDeps(lib):
    with open('Dependencies') as f:
        for line in f:
            dep=line.split(':')
            if dep[0] == lib:
                return dep[1].split()
    return []

def install(env, lib):
    deps=scanDeps(lib)
    for dep in deps:
        install(env, dep)

    sources=[]
    for root, dirnames, filenames in os.walk(lib+'/src'):
        for filename in fnmatch.filter(filenames, '*.c'):
            sources.append(Glob(os.path.join(root, filename)))

    env['CCFLAGS']=['-I'+lib+'/include/']

    staticLibrary=env.Library(target=lib+'/lib/'+lib, source=sources, LIBS=['m'])

    print 'Installing '+lib 
    libInstall=env.Install(dir='/usr/lib', source=staticLibrary)
    headerInstall=env.Install(dir='/usr/include', source=lib+'/include/'+lib)
    Clean(libInstall, '/usr/include/'+lib)
    env.Alias('install', '/usr')

env=DefaultEnvironment(CC='gcc')

# Scan all libraries
libraries=[]
for name in os.listdir('.'):
    if os.path.isdir(os.path.join('.', name)) and name[0] != '.':
        libraries.append(name)

opts=Variables('custom.py', ARGUMENTS)
opts.Add('target', ' '.join(map(str, libraries))+' none', 'none', allowed_values=libraries)
opts.Update(env)

if env['target'] != 'none':
    install(env, env['target'])

Help(opts.GenerateHelpText(env))
