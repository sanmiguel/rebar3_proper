Rebar3 Proper Plugin
=====

Run PropEr test suites.

By default, will look for all modules starting in `prop_` in the `test/`
directories of a rebar3 project, and running all properties (functions of arity
0 with a `prop_` prefix) in them.

Todo/Gotchas
----

- The plugin relies on the `1.1.1-beta` hex package of proper.
- No automated tests yet
- would like to find a way to store failed tests to a counterexample file
  that can be re-run at will rather than just using `--retry` on the
  latest failing case.

Use
---

Add the plugin to your rebar config:

    %% the plugin itself
    {plugins, [rebar3_proper]}.
    %% The PropEr dependency is still required to compile the test cases
    {profiles,
        [{test, [
            {deps, [{proper, "1.1.1-beta"}]}
        ]}
    ]}.

Then just call your plugin directly in an existing application:

    Usage: rebar3 proper [-d <dir>] [-m <module>] [-p <properties>]
                         [-n <numtests>] [-v <verbose>] [-c [<cover>]]
                         [--long_result <long_result>]
                         [--start_size <start_size>] [--max_size <max_size>]
                         [--max_shrinks <max_shrinks>]
                         [--noshrink <noshrink>]
                         [--constraint_tries <constraint_tries>]
                         [--spec_timeout <spec_timeout>]
                         [--any_to_integer <any_to_integer>]
    
      -d, --dir           directory where the property tests are located
                          (defaults to "test")
      -m, --module        name of one or more modules to test (comma-separated)
      -p, --prop          name of properties to test within a specified module
                          (comma-separated)
      -n, --numtests      number of tests to run when testing a given property
      -v, --verbose       each propertie tested shows its output or not
                          (defaults to true)
      -c, --cover         generate cover data [default: false]
      --retry             If failing test case counterexamples have been
                          stored, they are retried [default: false]
      --long_result       enables long-result mode, displaying
                          counter-examples on failure rather than just false
      --start_size        specifies the initial value of the size parameter
      --max_size          specifies the maximum value of the size parameter
      --max_shrinks       specifies the maximum number of times a failing test
                          case should be shrunk before returning
      --noshrink          instructs PropEr to not attempt to shrink any
                          failing test cases
      --constraint_tries  specifies the maximum number of tries before the
                          generator subsystem gives up on producing an
                          instance that satisfies a ?SUCHTHAT constraint
      --spec_timeout      duration, in milliseconds, after which PropEr
                          considers an input to be failing
      --any_to_integer    converts instances of the any() type to integers in
                          order to speed up execution

All of [PropEr's standard configurations](http://proper.softlab.ntua.gr/doc/proper.html#Options)
that can be put in a consult file can be put in `{proper_opts, [Options]}.` in your rebar.config file.


Changelog
----

- 0.7.2: rely on a non-beta PropEr version
- 0.7.1: fix bug regarding lib and priv directories in code path
- 0.7.0: fix bug with include paths of hrl files from parent apps, support counterexamples with --retry
- 0.6.3: fix bug with cover-compiling in rebar 3.2.0 and above again
- 0.6.2: fix bug with cover-compiling in rebar 3.2.0 and above
- 0.6.1: fix bug on option parsing in config files
- 0.5.0: switches to package dependencies
- 0.4.0: switches license to BSD with templates
- 0.3.0: code coverage supported
- 0.2.0: basic functionality
- 0.1.0: first commits
