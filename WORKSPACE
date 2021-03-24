workspace(name = "rules_perl")

load("@rules_perl//perl:deps.bzl", "perl_register_toolchains", "perl_rules_dependencies",)

perl_rules_dependencies()
perl_register_toolchains()

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "cache_memcached_fast",
    build_file = "//:examples/cpan_remote/cache_memcached_fast.BUILD",
    sha256 = "5e8e46d922cca6e4f385132c2cb2c71eef7f4b5ef58fbd36a399f9169deaa09a",
    strip_prefix = "Cache-Memcached-Fast-0.26",
    url = "https://cpan.metacpan.org/authors/id/R/RA/RAZ/Cache-Memcached-Fast-0.26.tar.gz",
)

http_archive(
    name = "fcgi",
    build_file = "//:examples/cpan_remote/fcgi.BUILD",
    sha256 = "8cfa4e1b14fb8d5acaa22ced672c6af68c0a8e25dc2a9697a0ed7f4a4efb34e4",
    strip_prefix = "FCGI-0.79",
    url = "https://cpan.metacpan.org/authors/id/E/ET/ETHER/FCGI-0.79.tar.gz",
)
