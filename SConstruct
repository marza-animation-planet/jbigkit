import glob
import excons

env = excons.MakeBaseEnv()

out_dir    = excons.OutputBaseDirectory()
out_incdir = out_dir + "/include"
out_libdir = out_dir + "/lib"

cmnhdr = env.Install(out_incdir, "libjbig/jbig_ar.h")

prjs = [
   {  "name": "jbig",
      "type": "staticlib",
      "srcs": ["libjbig/jbig.c",
               "libjbig/jbig_ar.c"],
      "install": {"include": ["libjbig/jbig.h"]}
   },
   {  "name": "jbig85",
      "type": "staticlib",
      "srcs": ["libjbig/jbig85.c",
               "libjbig/jbig_ar.c"],
      "install": {"include": ["libjbig/jbig85.h"]}
   }
]

excons.DeclareTargets(env, prjs)

env.Depends("jbig", cmnhdr)
env.Depends("jbig85", cmnhdr)


def RequireJbig(env):
   env.Append(CPPPATH=[out_incdir])
   env.Append(LIBPATH=[out_libdir])
   excons.StaticallyLink(env, "jbig85", silent=True)
   excons.StaticallyLink(env, "jbig", silent=True)

Export("RequireJbig")

