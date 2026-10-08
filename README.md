# rust-chip8

A CHIP-8 emulator written in Rust.

## Structure

- `core/` — the emulator itself (CPU, memory, opcodes), as a library crate.
- `desktop/` — native desktop frontend using SDL2.
- `wasm/` — WebAssembly bindings around `core`, for running in a browser.
- `web/` — static site (HTML/JS) that loads the wasm build and renders to a `<canvas>`.

## ROMs

ROM files aren't included in this repo to avoid any copyright ambiguity. Place CHIP-8 ROMs in a `roms/` directory at the project root (ignored by git) and point the desktop binary at one:

```
cargo run --manifest-path desktop/Cargo.toml -- roms/PONG
```

ROM packs are easy to find online by searching for "CHIP-8 ROMs" or "CHIP-8 games pack".

## Running in the browser

The wasm build output isn't committed (it's generated), so build it yourself and copy it alongside the static site:

```
cd wasm
wasm-pack build --target web
cp pkg/wasm.js pkg/wasm_bg.wasm ../web/
```

Then serve `web/` with any static file server (e.g. `python3 -m http.server`, run from inside `web/`) and open it in a browser. Use the file picker on the page to load a ROM.
