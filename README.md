# vcpkg-registry

Package registry for AVGT, containing ports for packages that cannot be obtained from the official `vcpkg` repository, either due to incompatibilities, or where an official port doesn't exist at all.

## Contained packages

| Package                                         | Reason                                                                                                                                                                               |
| ----------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [OpenVPN3](https://github.com/OpenVPN/openvpn3) | The version from the official vcpkg repository was outdated. Now, both packages are on the same version (3.7.0), but they are not compatible, so we'll stick using our port for now. |
