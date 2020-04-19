Debian / Ubuntu package for meshoptimizer
=========================================

Prerequisites: `dpkg-dev`, `debhelper`

The building is done in-source, meaning it will pack whatever branch, commit
and working copy change you're currently on. Clone the repository and run the
following command:

```sh
git clone https://github.com/zeux/meshoptimizer
cd meshoptimizer
dpkg-buildpackage -j8
```

THe build may fail with the following if you don't have signing keys set up,
which can be safely ignored -- the `*.deb` packages are correctly produced in
this case as well:

> dpkg-buildpackage: error: failed to sign .dsc and .changes file

A binary package (with the `*.so` and a `gltfpack` executable) and a `-dev`
package (with includes and CMake modules) is made, similarly to how common
`*.deb` packages are split as well. The files are generated one level up,
install them directly via `dpkg`:

```sh
sudo dpkg -i ../meshoptimizer*.deb
```

Bumping the version for a new release
-------------------------------------

This has to be done by *prepending* a new entry to the `debian/changelog` file.
The system is extremely picky about whitespace, special characters and
formatting, so the least error-prone way is to verbatim copy the last entry,
put it first in the file separated by a blank line from the rest, and update
the version number and the date as well. The date *has to be* in the same
format as is produced by `date -R` and has to be separated by exactly two
spaces from the name and e-mail. (Sorry, I didn't invent those rules.)

The version bump should be done ideally before adding a git tag, so the tagged
commit can be used directly to produce a package.
