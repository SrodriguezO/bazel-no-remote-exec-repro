Test against any remote execution cluster. 
I used the simple Buildfarm cluster explained in their [Quick Start Wiki (remote execution section)](https://github.com/bazelbuild/bazel-buildfarm/wiki/Quick-Start#remote-execution-and-caching)

From this workspace, run:
```
bazelisk build :main --remote_cache=<re cluster> --experimental_allow_tags_propagation
bazelisk clean
bazelisk build :main --remote_cache=<re cluster> --experimental_allow_tags_propagation
```
You should see cache hits

Now run:
```
bazelisk build :main --remote_executor=<re cluster> --experimental_allow_tags_propagation
bazelisk clean
bazelisk build :main --remote_executor=<re cluster> --experimental_allow_tags_propagation
```
You should not see cache hits.


Attribution: 
The code in this repo was borrowed from the Buildfarm [Quick Start Wiki](https://github.com/bazelbuild/bazel-buildfarm/wiki/Quick-Start), with the `tags = ["no-remote-exec"]` stuff and the `.bazelversion` file added.
