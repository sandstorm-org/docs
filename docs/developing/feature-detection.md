# Feature detection

There are now multiple different versions of Sandstorm available in the
wild. At present, most have fairly common code, and we expect most API
features of Sandstorm to be widely supported. However, a developer may
need to adjust app behavior based on support for different Sandstorm
versions or runtimes.

Sandstorm implementations are generally expected to run with an evergreen
update model and automatic updates. This means developers should assume
a given platform supports the latest version of the code for that
distribution.

The first community release of Sandstorm, build 309, introduces a new
`SERVER_RUNTIME` environment variable, which returns `classic`. This
indicates to the app that it is running on the modern community release
of Sandstorm, and includes any features introduced after this fork. The
absence of this environment variable should be treated as the feature set
of the original Sandstorm.io platform, of which its final version was 308.

When Tempest is available, it will return a value of `tempest`.

## Implementing a fork with app platform features

The Sandstorm project welcomes forks. If a forked codebase adds additional
app platform API features, we recommend they [modify this value](https://github.com/sandstorm-io/sandstorm/pull/3766)
which can only be changed in the source code. By encouraging apps to check
the value of `SERVER_RUNTIME` prior to invoking custom API features, apps
can be built which support multiple implementations of the platform, and
are eligible to be included in and distributed by the Sandstorm app market.

Do not use this feature as part of a proprietary app licensing scheme. The
Sandstorm team may allow users to override this setting on specific apps if
it is needed to bypass improper feature detection code.