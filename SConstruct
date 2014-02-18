# -*- python -*-

vars = Variables()
vars.Add(PathVariable('PREFIX', 'prefix used to install files', '/usr'))
vars.Add(PathVariable('JSONCPP', 'path of jsoncpp library', None))

env = Environment(variables = vars)

env["CPPFLAGS"] = ["-O2", "-Wall", "-Werror", "-Wshadow", "-std=c++11", "-pthread"]
env["CPPPATH"] = [Dir("include"), Dir("src")]
env["LIBPATH"] = []

# jsoncpp library
if "JSONCPP" in env :
    env["CPPPATH"] += ["%s/include" % env["JSONCPP"]]
    env["LIBPATH"] += ["%s/lib" % env["JSONCPP"]]

env["SHCXXCOMSTR"] = "Compiling $SOURCE"
env["SHLINKCOMSTR"] = "Linking $TARGET"

if "PREFIX" in env :
    env["CPPPATH"] += ["%s/include" % env["PREFIX"]]

plugin = env.SharedLibrary(
    target = "http-server",
    source = ["src/plugin.cpp", "src/server.cpp", "src/request.cpp", "src/response.cpp"],
    LIBS = ["microhttpd"]
)

env.Alias("install", env.Install("$PREFIX/lib/zeppelin/plugins", plugin))
env.Alias("install", env.Install("$PREFIX/include/zeppelin/plugins/http-server", "include/http-server/httpserver.h"))
