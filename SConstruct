import os

env = SConscript("godot-cpp/SConstruct")
gype_target = ARGUMENTS.get('gype_target')

def get_sources(path):
    sources = []
    for root, dirs, files in os.walk(path):
        sources += Glob(os.path.join(root, '*.cpp'))
    for root, dirs, files in os.walk(path):
        sources += Glob(os.path.join(root, '*.c'))
    return sources

if os.name == 'nt':
    prebuilt_path = "windows-x86_64"
elif os.name == 'posix':
    prebuilt_path = "linux-x86_64"
else:
    raise OSError("Unsupported operating system")

if gype_target == 'windows':
    env["LINK"]="g++"
elif gype_target == 'linux':
    env["LINK"]="g++"
elif gype_target == 'android':
    pass
else:
    print(f"gype_target is an unexpected value: {gype_target}")

env.Append(CFLAGS=["-O3"])
env.Append(CXXFLAGS=["-std=c++17", "-O3"])
env.Append(CPPPATH=[
    "include", 
    "godot-cpp/include", 
    "godot-cpp/gen/include"
    ])

sources = []
sources.extend(get_sources('src'))
sources.extend(get_sources('godot-cpp/src'))
sources.extend(get_sources('godot-cpp/gen/src'))

library = env.SharedLibrary(
    "bin/libgype{}{}".format(env["suffix"], env["SHLIBSUFFIX"]),
    source=[]
)

Default([library])
