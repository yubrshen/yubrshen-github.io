
# Table of Contents

-   [The problem](#org94c9b3c)
-   [The solution](#org9f79844)
-   [Source of confusion](#orgca5c158)
-   [Limitation](#org77be072)



<a id="org94c9b3c"></a>

# The problem

A project with ClojureScript and Shadow-cljs started with a standalone REPL.
One needs to use M-x cider-connect-cljs from emacs to the externally started REPL.
The problem is when executing M-x cider-connect-cljs, the only feedback is the message in the message buffer of emacs:

    [nREPL] Establishing direct connection to localhost:9001 ...
    [nREPL] Direct connection to localhost:9001 established

but the REPL is actually not working that in a buffer of ClojureScript source code of the project that the REPL has been started for,
evaluation of expression does not produce with value.


<a id="org9f79844"></a>

# The solution

Suppose, the command to start the standalone REPL is

    clojure -m serve

where &rsquo;serve&rsquo; is the alias for the program to be started.

Then the deps.edn must have dependencies required for cider to connect to the REPL via cider.nrepl protocol:

    {:paths ["src" "resources"]
     :deps {org.clojure/clojure    {:mvn/version "1.10.3"}
            com.fulcrologic/fulcro {:mvn/version "3.4.22"}
            com.wsscode/pathom     {:mvn/version "2.3.1"}}
     :aliases
     {:serve {:main-opts ["-m" "shadow.cljs.devtools.cli" "watch" "main"]
              :extra-deps {thheller/shadow-cljs                {:mvn/version "2.11.14"}
                           binaryage/devtools                  {:mvn/version "1.0.0"}
                           org.clojure/clojurescript {:mvn/version "1.10.773"} ; seems optional for M-x cider-connect-cljs
                           cider/cider-nrepl {:mvn/version "0.25.9"}           ; must be added for M-x cider-connect-cljs
                           cider/piggieback {:mvn/version "0.5.1"}             ; seems optional for M-x cider-connect-cljs
                           }}}}

For each alias for a main program (here &rsquo;serve&rsquo;), those dependencies must be added.

This note of observation is confirmed on May 29, 2021. The duration of the validity might be limited.

<a id="orgca5c158"></a>

# Source of confusion

At [Setting Up a Standalone REPL:Using tools.deps](https://docs.cider.mx/cider/basics/middleware_setup.html#using-tools-deps)
it has alluded to the idea, but it&rsquo;s not clear for beginner, and the configuraiton is outdated:

    You can add the following aliases to your deps.edn in order to launch a standalone Clojure(Script) nREPL server with CIDER middleware from the commandline with something like clj -A:cider-clj. Then from emacs run cider-connect or cider-connect-cljs.

    :cider-clj {:extra-deps {cider/cider-nrepl {:mvn/version "0.22.4"}}
                :main-opts ["-m" "nrepl.cmdline" "--middleware" "[cider.nrepl/cider-middleware]"]}
    
    :cider-cljs {:extra-deps {org.clojure/clojurescript {:mvn/version "1.10.339"}
                              cider/cider-nrepl {:mvn/version "0.22.4"}
                              cider/piggieback {:mvn/version "0.5.1"}}
                 :main-opts ["-m" "nrepl.cmdline" "--middleware"
                             "[cider.nrepl/cider-middleware,cider.piggieback/wrap-cljs-repl]"]}

I figured the solution based on my experiment, and hint from [nREPL](https://shadow-cljs.github.io/docs/UsersGuide.html#nREPL) of Shadow-cljs server:

    If the popular middleware cider-nrepl is found on the classpath (e.g. it’s included in :dependencies), it will be used automatically. No additional configuration required.

The options in :main-opts for ClojureScript is no longer needed.
(It remains a question, how to configure for Clojure support Shadow-cljs. So far, my experiment project does not involve Clojure.
Shadow-cljs is meant to support ClojureScript compilation, maybe, there is no need for middleware configuration for Clojure?)


<a id="org77be072"></a>

# Limitation

The above deps.edn may not work yet for a REPL to be started within emacs by M-x cider-jack-in-cljs

I wish any expert can shed more light on more understanding of the rationals of the proper configuration for ClojureScript with Shadow-cljs to work with cider/emacs.
There are many documentations on Shadow-cljs/cider, but they are scattered, maybe outdated, and not accessible to beginners.

