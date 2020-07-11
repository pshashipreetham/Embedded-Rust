# Embedded Rust based Led Blink on NUCLEOF446RE


**OS:** Ubuntu 18.04<br/>
**Board:** NUCLEOF446RE<br/>
**Programming:** [Embedded Rust](https://rust-embedded.github.io/book/)<br/>
**Prerequisites:** <br/>
- [x] [Rust](https://rust-embedded.github.io/book/)<br/>
- [x] [Openocd](http://openocd.org/doc/html/GDB-and-OpenOCD.html)</br>

**Rust Installation:**
```sh
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```
I also recommend installing the cargo-generate and cargo-binutils packages. They provide some helpful tools to get up and running quickly with new projects, and to simplify debugging. They can (optionally) be installed by running the following:
```rust
cargo install cargo-generate cargo-binutils
rustup component add llvm-tools-preview  # for cargo-binutils
```

With both Rust and Cargo installed and configured, it's time to OpenOCD and GDB, there may be multiple versions of GDB available; just ensure it's compatible with ARM. 
On **Ubuntu 18.04** you can use the **gdb-multiarch package**:
```console
sudo apt update
sudo apt install -y openocd gdb-multiarch
```
**Let's get started with the project:**
```console
rustup target add thumbv7em-none-eabihf
git clone https://github.com/psp316r/Embedded-Rust.git
cd Embedded-Rust
cargo build --release
```
To upload code to the Board I am using [Openocd](http://openocd.org/doc/html/GDB-and-OpenOCD.html)

----> In **terminal 1** use following commands:
```rust
cd Embedded-Rust
arm-none-eabi-gdb target/thumbv7em-none-eabihf/release/blinky
```

----> In **terminal 2** open openocd connection by follwoing Command
```rust
cd Embedded-Rust
openocd -f openocd.cfg
```

---->In **terminal 1** again I used following commands
```rust
target remote: 3333
```

---->after this to flash the code, I have used following command in **terminal 1**
```rust
load
```
---->To Create **.bin** File of the Project

```rust
cargo objcopy --bin blinky --release -- -O binary target/thumbv7em-none-eabihf/release/blinky.bin
```

**Project References:**</br>
[cortex_m_quickstart](https://docs.rs/cortex-m-quickstart/0.2.7/cortex_m_quickstart/)</br>
