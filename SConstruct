import fnmatch
import os

env=Environment(CC='gcc', CCFLAGS='-Iinclude/')

# Scan all libraries
libraries=[]
for name in os.listdir('.'):
    if os.path.isdir(os.path.join('.', name)) and (name[0] != '.'):
        libraries.append(name)

opts=Variables('custom.py', ARGUMENTS)
opts.Add('target', ' '.join(map(str, libraries)), libraries[0], allowed_values='')
opts.Update(env)

Help(opts.GenerateHelpText(env))
