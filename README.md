# What?
secp256k1 added to Golang crypto/elliptic

This is copied from this PR:
https://github.com/golang/go/pull/26873

The parent issue was rejected and closed here with this comment:
https://github.com/golang/go/issues/26776#issuecomment-498069425
```
I am saying the standard library should provide specialized implementations of an opinionated
small set of curves, not support for all possible curves. The latter belongs in a third-party
project (which can absolutely start from the stdlib code, as it's BSD licensed).
```

# Why?

You can use a golang lib that wraps a bunch of C headers from who knows where, or you can use this.

All you need to trust is the PR above.

# Tests
```
git clone git@github.com:eliwjones/crypto.git
cd crypto
go test -v ./...
?   	github.com/eliwjones/crypto	[no test files]
=== RUN   TestKeyGeneration
--- PASS: TestKeyGeneration (0.02s)
=== RUN   TestSignAndVerify
--- PASS: TestSignAndVerify (0.09s)
=== RUN   TestNonceSafety
   .
   .
   .
```

# Example
```
# To see a working example
go run main.go
signature: (0x77d18512ce3462002feeeb9d340f8f3f073bdecf1032f062867c3a0119dd5362, 0x91b6d18b61bfa3501434c7f7ea28554adefb32225d2b9c6fcf34f76d105621a3)
signature verified: true
```

# How do I verify this hasn't been changed from the PR?
```
git clone git@github.com:eliwjones/crypto.git
git clone git@github.com:golang/go.git go_master
cd go_master && git checkout a0127c1921 && cd ..  # get code from when this patch was made.
cp go_master/src/crypto/elliptic/* crypto/elliptic/.
cp -r go_master/src/crypto/ecdsa/* crypto/ecdsa/.
cd ~/crypto && git diff
```