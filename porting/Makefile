BIN_LIST = blink.bin
TARGET_LIST = blink

all: $(BIN_LIST)

FLASH_TARGETS = $(addprefix flash-,$(TARGET_LIST))

$(FLASH_TARGETS): $(BIN_LIST)
	openocd \
		-f interface/stlink-v2-1.cfg \
		-f target/stm32f4x.cfg \
		-c "init" \
		-c "reset init" \
		-c "stm32f2x unlock 0" \
		-c "flash probe 0" \
		-c "flash info 0" \
		-c "flash write_image erase $(@:flash-%=%).bin 0x8000000" \
		-c "reset run" -c shutdown || \
	st-flash write $(@:flash-%=%).bin 0x8000000
clean:
	rm -f $(BIN_LIST)
