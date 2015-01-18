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

    print 'Installing ' + lib 
    libInstall=env.Install(dir='/usr/lib', source=lib + '/lib/lib' + lib + '.a')
    headerInstall=env.Install(dir='/usr/include', source=lib + '/include/' + lib)
    Clean(libInstall, '/usr/include/' + lib)
    env.Alias('install', '/usr')
    

env=Environment(CC='gcc', CCFLAGS='-Iinclude/')

# Scan all libraries
libraries=[]
for name in os.listdir('.'):
    if os.path.isdir(os.path.join('.', name)) and name[0] != '.':
        libraries.append(name)

opts=Variables('custom.py', ARGUMENTS)
opts.Add('target', ' '.join(map(str, libraries)), libraries[0], allowed_values=libraries)
opts.Update(env)

install(env, env['target'])

Help(opts.GenerateHelpText(env))
