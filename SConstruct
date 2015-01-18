import fnmatch
import os

def scanDependencies(library):
    with open('Dependencies') as f:
        for line in f:
            dep=line.split(':')
            if dep[0] == library:
                return dep[1].strip().split(',')
    return []


env=Environment(CC='gcc', CCFLAGS='-Iinclude/')

# Scan all libraries
libraries=[]
for name in os.listdir('.'):
    if os.path.isdir(os.path.join('.', name)) and name[0] != '.':
        libraries.append(name)

opts=Variables('custom.py', ARGUMENTS)
opts.Add('target', ' '.join(map(str, libraries)), libraries[0], allowed_values=libraries)
opts.Update(env)

# Load the dependencies from the 'Dependencies' file
print ' '.join(scanDependencies(env['target']))

Help(opts.GenerateHelpText(env))
