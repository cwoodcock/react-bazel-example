workspace(name = "react_samples")

http_archive(
    name = "build_bazel_rules_nodejs",
    url = "https://github.com/bazelbuild/rules_nodejs/archive/0.16.0.zip",
    strip_prefix = "rules_nodejs-0.16.0",
)

# The Bazel buildtools repo contains tools like the BUILD file formatter, buildifier
http_archive(
    name = "com_github_bazelbuild_buildtools",
    # Note, this commit matches the version of buildifier in angular/ngcontainer
    url = "https://github.com/bazelbuild/buildtools/archive/7926f6cd8f2568556b0efc23530743df4278e0fe.zip",
    strip_prefix = "buildtools-7926f6cd8f2568556b0efc23530743df4278e0fe",
)

# Runs the TypeScript compiler
http_archive(
    name = "build_bazel_rules_typescript",
    url = "https://github.com/bazelbuild/rules_typescript/archive/0.20.3.zip",
    strip_prefix = "rules_typescript-0.20.3",
)
load("@build_bazel_rules_typescript//:package.bzl", "rules_typescript_dependencies")
rules_typescript_dependencies()

load("@io_bazel_rules_go//go:def.bzl", "go_rules_dependencies", "go_register_toolchains")
go_rules_dependencies()
go_register_toolchains()
load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies")
gazelle_dependencies()

maven_jar(
    name = "protobuf_java_format",
    artifact = "com.googlecode.protobuf-java-format:protobuf-java-format:1.4",
    sha1 = "b8163b6940102c1808814471476f5293dfb419df",
)

# java_lite_proto_library rules implicitly depend on @com_google_protobuf_javalite//:javalite_toolchain,
# which is the JavaLite proto runtime (base classes and common utilities).
http_archive(
    name = "com_google_protobuf_javalite",
    sha256 = "d8a2fed3708781196f92e1e7e7e713cf66804bd2944894401057214aff4f468e",
    strip_prefix = "protobuf-5e8916e881c573c5d83980197a6f783c132d4276",
    urls = ["https://github.com/google/protobuf/archive/5e8916e881c573c5d83980197a6f783c132d4276.zip"],
)

http_archive(
    name = "io_bazel_rules_appengine",
    strip_prefix = "rules_appengine-0.0.8",
    url = "https://github.com/bazelbuild/rules_appengine/archive/0.0.8.tar.gz",
)
load("@io_bazel_rules_appengine//appengine:java_appengine.bzl", "java_appengine_repositories")
java_appengine_repositories()

# load("@io_bazel_rules_appengine//appengine:appengine.bzl", "appengine_repositories")
# appengine_repositories()

load("@build_bazel_rules_nodejs//:defs.bzl", "check_bazel_version", "node_repositories", "yarn_install")

node_repositories(package_json = ["//:package.json"])

load("@io_bazel_rules_webtesting//web:repositories.bzl", "browser_repositories", "web_test_repositories")

load("@build_bazel_rules_typescript//:defs.bzl", "ts_setup_workspace")
ts_setup_workspace()

yarn_install(
  name = "npm",
  package_json = "//:package.json",
  yarn_lock = "//:yarn.lock",
)
