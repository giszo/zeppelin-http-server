# -*- python -*-

AddOption(
    "--prefix",
    dest = "prefix",
    type = "string",
    nargs = 1,
    action = "store",
    metavar = "DIR",
    help = "installation prefix")
AddOption(
    "--zeppelin",
    dest = "zeppelin",
    type = "string",
    nargs = 1,
    action = "store",
    metavar = "DIR",
    help = "zeppelin installation path")

env = Environment(PREFIX = GetOption("prefix"))

env["CPPFLAGS"] = ["-O2", "-Wall", "-Werror", "-Wshadow", "-std=c++11", "-pthread"]
env["CPPPATH"] = [Dir("include"), Dir("src")]

if GetOption("zeppelin") :
    env["CPPPATH"] += ["%s/%s" % (GetOption("zeppelin"), "/usr/include")]

plugin = env.SharedLibrary(
    target = "http-server",
    source = ["src/plugin.cpp", "src/server.cpp", "src/request.cpp", "src/response.cpp"],
    LIBS = ["microhttpd"]
)

env.Alias("install", env.Install("$PREFIX/usr/lib/zeppelin/plugins", plugin))
env.Alias("install", env.Install("$PREFIX/usr/include/zeppelin/plugins/http-server", "include/http-server/httpserver.h"))
