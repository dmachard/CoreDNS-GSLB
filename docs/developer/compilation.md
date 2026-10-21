# Binary Compilation

To run CoreDNS-GSLB, you must build a custom CoreDNS binary that compiles the `gslb` plugin.

CoreDNS-GSLB currently targets **CoreDNS v1.15.0** and requires **Go 1.26 or later**.

## Step 1: Update plugin configuration

1. Clone the CoreDNS source code and check out the supported version:

```bash
git clone https://github.com/coredns/coredns.git
cd coredns
git checkout v1.15.0
```

2. Edit the file `plugin.cfg` inside the CoreDNS source directory.
3. Register the `gslb` plugin by adding the following line. It is recommended to place it right before `file:file` to ensure proper routing priority:

```text
gslb:github.com/dmachard/coredns-gslb
```

## Step 2: Compile the Binary

Add the plugin dependency, then run code generation and compile CoreDNS:

```bash
go get github.com/dmachard/coredns-gslb
go generate
make
```

This compiles a `coredns` executable with the GSLB plugin compiled in. You can run and configure it using standard Corefiles.
