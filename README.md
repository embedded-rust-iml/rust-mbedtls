# mbedtls

Forked from https://github.com/fortanix/rust-mbedtls. In this current branch, the configuration of
the underlying mbedtls C-library is changed in a hard-coded way to leave out a considerable amount
of features. This is done to drastically reduce the code size to enable usage on small MCUs.
Specifically, this has been done to enable usage in the
[Sensing Puck](https://www.silicon-economy.com/en/project/sensing-puck-en/).

With the configuration in this branch, this library can only be used for (D)TLS clients with the
TLS_PSK_WITH_AES_128_CCM_8 cipher suite. So all server-side code, all public-key cryptography and
all other cryptographic suites were removed. This was accomplished by changing the relatively
hard-coded configuration in `mbedtls-sys/build/config.rs`. Due to these changes, the Rust wrapper
code which used the now missing functions was commented-out to avoid build errors.

The changes were made like this to quickly enable usage on small MCUs. In the future, a proper
solution which enables flexible build-time configuration for different use cases is planned but this
will require quite some changes and good coordination with the upstream maintainers.

## Contact

Fraunhofer IML Embedded Rust Group - <embedded-rust@iml.fraunhofer.de>
