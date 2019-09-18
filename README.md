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

# How do I verify this hasn't been changed from the PR?
```
cd ~
git clone git@github.com:eliwjones/elliptic.git
git clone git@github.com:golang/go.git go_master
cp ~/go_master/src/crypto/elliptic/* ~/elliptic/.
cd ~/elliptic && git diff
```
