BOARD ?= nk3xn

FEATURES := board-${BOARD},develop

.PHONY: build-dev
build-dev:
	cargo build --release --features $(FEATURES)

.PHONY: run-dev
run-dev:
	cargo run --release --features $(FEATURES)

.PHONY: objcopy-dev
objcopy-dev:
	cargo objcopy --release --features $(FEATURES) -- -O binary "firmware-${BOARD}.bin"

.PHONY: flash-dev
flash-dev: objcopy-dev
	mboot erase --mass
	mboot write "firmware-${BOARD}.bin"

bacon:
	bacon


PACK_VERSION := $(shell wget -O - -qq https://mcuxpresso.nxp.com/cmsis_pack/repo/NXP.pidx|grep LPC55S69|python -c'import sys; print(sys.stdin.read().rsplit("version=\"", 1)[1].split("\"", 1)[0])')
PACK := NXP.LPC55S69_DFP.$(PACK_VERSION).pack
get-cmsis-pack:
	wget -qq https://mcuxpresso.nxp.com/cmsis_pack/repo/$(PACK) -O ./lpc55s69.pack

