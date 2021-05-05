import sys
import glob
import excons
import SCons.Script # pylint: disable=import-error

env = excons.MakeBaseEnv()

out_dir    = excons.OutputBaseDirectory()
out_incdir = out_dir + "/include"
out_libdir = out_dir + "/lib"

def JbigName():
   return ("lib" if sys.platform == "win32" else "") + "jbig"

def JbigPath():
   name = JbigName()
   if sys.platform == "win32":
      libname = name + ".lib"
   else:
      libname = "lib" + name + ".a"
   return out_libdir + "/" + libname

def RequireJbig(env):
   env.Append(CPPPATH=[out_incdir])
   env.Append(LIBPATH=[out_libdir])
   excons.Link(env, JbigPath(), static=True, force=True, silent=True)

def Jbig85Name():
   return ("lib" if sys.platform == "win32" else "") + "jbig85"

def Jbig85Path():
   name = Jbig85Name()
   if sys.platform == "win32":
      libname = name + ".lib"
   else:
      libname = "lib" + name + ".a"
   return out_libdir + "/" + libname

def RequireJbig85(env):
   env.Append(CPPPATH=[out_incdir])
   env.Append(LIBPATH=[out_libdir])
   excons.Link(env, Jbig85Path(), static=True, force=True, silent=True)

cmnhdr = env.Install(out_incdir, "libjbig/jbig_ar.h")

prjs = [
   {  "name": JbigName(),
      "alias": "jbig",
      "type": "staticlib",
      "srcs": ["libjbig/jbig.c",
               "libjbig/jbig_ar.c"],
      "install": {"include": ["libjbig/jbig.h"]}
   },
   {  "name": Jbig85Name(),
      "alias": "jbig85",
      "type": "staticlib",
      "srcs": ["libjbig/jbig85.c",
               "libjbig/jbig_ar.c"],
      "install": {"include": ["libjbig/jbig85.h"]}
   }
]

excons.DeclareTargets(env, prjs)

env.Depends("jbig", cmnhdr)
env.Depends("jbig85", cmnhdr)

SCons.Script.Export("JbigName JbigPath RequireJbig Jbig85Name Jbig85Path RequireJbig85")

