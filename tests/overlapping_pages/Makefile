#
# Copyright 2021, Breakaway Consulting Pty. Ltd.
#
# SPDX-License-Identifier: BSD-2-Clause
#
LIBSEL4CP := ../../libsel4cp
TOOLCHAIN := aarch64-linux-gnu

CPU := cortex-a53

CC := $(TOOLCHAIN)-gcc
LD := $(TOOLCHAIN)-ld
AS := $(TOOLCHAIN)-as

OVERLAPPING_PAGES_OBJS := overlapping_pages.o

IMAGES := overlapping_pages.elf
CFLAGS := -mcpu=$(CPU) -mstrict-align -nostdlib -ffreestanding -g3 -O3 -Wall  -Wno-unused-function -Werror -I$(SEL4_SDK)/include -I$(LIBSEL4CP)/include
LDFLAGS := -L$(LIBSEL4CP) -Tsel4cp.ld
LIBS := -lsel4cp


all: $(IMAGES)

%.o: %.c Makefile
	$(CC) -c $(CFLAGS) $< -o $@

%.o: %.s Makefile
	$(AS) -g3 -mcpu=$(CPU) $< -o $@

overlapping_pages.elf: $(OVERLAPPING_PAGES_OBJS)
	$(LD) $(LDFLAGS) $(OVERLAPPING_PAGES_OBJS) $(LIBS) -o $@
