# SPDX-License-Identifier: GPL-2.0

obj-m := gaming.o

gaming.ko: gaming.c
		make -C /usr/src/linux-headers-`uname -r` M=`pwd` V=1 modules

clean:
		make -C /usr/src/linux-headers-`uname -r` M=`pwd` V=1 clean
