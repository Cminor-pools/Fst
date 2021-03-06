Fastcoin Core [FST]

==========================
What is Fastcoin?

Fastcoin (FST) has a long history after being created in May 2013 in order to provide faster and less expensive payments than Bitcoin. As a community coin, the project received significant support in 2021 and was rebased on Dogecoins codebase, making it AUX-POW with other security features. 60 second Block times, DigiShield, tremendous chain work and very low fees are what Fastcoin offers. This and maximum Cheetah presence ;) Ironically, it is similar to another popular Internet meme coin that began 7 months after FST. The open-source digital currency was began in Toronto Canada and was forked from Litecoin in May 2013, then rebased off Dogecoin in 2021. Fastcoin's creators envisaged it as a faster, lesser expensive and more transactional cryptocurrency that would have greater appeal beyond the core Bitcoin audience, did we mention it has maximum Cheetah?

http://fastcoin-project.com/
License

Fastcoin Core is released under the terms of the MIT license. See COPYING for more information or see https://opensource.org/licenses/MIT.
Development and contributions

Development is ongoing, and the development team, as well as other volunteers, can freely work in their own trees and submit pull requests when features or bug fixes are ready.
Version strategy

Version numbers are following major.minor.patch semantics.
Branches

There are 3 types of branches in this repository:

    master: Stable, contains the latest version of the latest major.minor release.
    maintenance: Stable, contains the latest version of previous releases, which are still under active maintenance. Format: <version>-maint
    development: Unstable, contains new code for planned releases. Format: <version>-dev

Master and maintenance branches are exclusively mutable by release. Planned releases will always have a development branch and pull requests should be submitted against those. Maintenance branches are there for bug fixes only, please submit new features against the development branch with the highest version.
Contributions

Developers are strongly encouraged to write unit tests for new code, and to submit new unit tests for old code. Unit tests can be compiled and run (assuming they weren't disabled in configure) with: make check. Further details on running and extending unit tests can be found in /src/test/README.md.

There are also regression and integration tests of the RPC interface, written in Python, that are run automatically on the build server. These tests can be run (if the test dependencies are installed) with: qa/pull-tester/rpc-tests.py

Changes should be tested by somebody other than the developer who wrote the code. This is especially important for large or high-risk changes. It is useful to add a test plan to the pull request description if testing the changes is not straightforward.
How to make fastcoind/fastcoin-cli/fastcoin-qt

The following are developer notes on how to build Fastcoin on your native platform. They are not complete guides, but include notes on the necessary libraries, compile flags, etc.

    OSX Build Notes
    Unix Build Notes
    Windows Build Notes

Fastcoin ports

RPC 9527 P2P 9526

Ubuntu compiling with boost_1.65.1

cd fastcoin
BITCOIN_ROOT=$(pwd)
BDB_PREFIX="${BITCOIN_ROOT}/db5"
mkdir -p $BDB_PREFIX
wget 'http://download.oracle.com/berkeley-db/db-5.1.29.NC.tar.gz'
echo '08238e59736d1aacdd47cfb8e68684c695516c37f4fbe1b8267dde58dc3a576c db-5.1.29.NC.tar.gz' | sha256sum -c
tar -xzvf db-5.1.29.NC.tar.gz
cd db-5.1.29.NC/build_unix/
../dist/configure --enable-cxx --disable-shared --with-pic --prefix=$BDB_PREFIX
make install
cd $BITCOIN_ROOT
./autogen.sh
./configure LDFLAGS="-L${BDB_PREFIX}/lib/" CPPFLAGS="-I${BDB_PREFIX}/include/" --disable-tests --disable-bench --enable-upnp-default
make

compiling for debugging

Run configure with the --enable-debug option, then make. Or run configure with CXXFLAGS="-g -ggdb -O0" or whatever debug flags you need.

debug.log

If the code is behaving strangely, take a look in the debug.log file in the data directory; error and debugging messages are written there.

The -debug=... command-line option controls debugging; running with just -debug will turn on all categories (and give you a very large debug.log file).

The Qt code routes qDebug() output to debug.log under category "qt": run with -debug=qt to see it.

testnet and regtest modes

Run with the -testnet option to run with "play fastcoins" on the test network, if you are testing multi-machine code that needs to operate across the internet.

If you are testing something that can run on one machine, run with the -regtest option. In regression test mode, blocks can be created on-demand; see qa/rpc-tests/ for tests that run in -regtest mode.

DEBUG_LOCKORDER

Fastcoin Core is a multithreaded application, and deadlocks or other multithreading bugs can be very difficult to track down. Compiling with -DDEBUG_LOCKORDER (configure CXXFLAGS="-DDEBUG_LOCKORDER -g") inserts run-time checks to keep track of which locks are held, and adds warnings to the debug.log file if inconsistencies are detected.
