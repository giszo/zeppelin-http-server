# -*- python -*-

vars = Variables()
vars.Add(PathVariable('PREFIX', 'prefix used to install files', '/usr'))

env = Environment(variables = vars)

env["CPPFLAGS"] = ["-O2", "-Wall", "-Werror", "-Wshadow", "-std=c++11", "-pthread"]
env["CPPPATH"] = [Dir("include"), Dir("src")]

if "PREFIX" in env :
    env["CPPPATH"] += ["%s/include" % env["PREFIX"]]

plugin = env.SharedLibrary(
    target = "http-server",
    source = ["src/plugin.cpp", "src/server.cpp", "src/request.cpp", "src/response.cpp"],
    LIBS = ["microhttpd"]
)

env.Alias("install", env.Install("$PREFIX/lib/zeppelin/plugins", plugin))
env.Alias("install", env.Install("$PREFIX/include/zeppelin/plugins/http-server", "include/http-server/httpserver.h"))
