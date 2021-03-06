#*******************************************************************************
# Copyright (C) 2010   STMicroelectronics. All Rights Reserved.
# This file is part of the latest release of the Multicom4 project. This release 
# is fully functional and provides all of the original MME functionality.This 
# release  is now considered stable and ready for integration with other software 
# components.

 # Multicom4 is a free software; you can redistribute it and/or modify it under the 
# terms of the GNU General Public License as published by the Free Software Foundation 
# version 2.

# Multicom4 is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; 
# without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. 
# See the GNU General Public License for more details.

# You should have received a copy of the GNU General Public License along with Multicom4; 
# see the file COPYING.  If not, write to the Free Software Foundation, 59 Temple Place - 
# Suite 330, Boston, MA 02111-1307, USA.

# Written by Multicom team at STMicroelectronics in November 2010.  
# Contact multicom.support@st.com. 
#*******************************************************************************

#
# Linux specific Makefile for ICS subsystem module
#
#

ifneq ($(KERNELRELEASE),)

#
# Inside Linux kernel tree
#

obj-m   := ics.o ics_user.o

# ICS specific CFLAGS
EXTRA_CFLAGS += -I$(obj)/../../include -I$(obj)/../../include/bsp -I$(obj)/include  $(DEBUG_CFLAGS) $(MULTICOM_EXTRA_CFLAGS)

# Allow a non local BSP source directory.
# PATH specified must be relative to this directory though
BSP_SRCDIR ?= ../bsp

# Assume defualt cpu as st40 .. then change it based in SOC type.
defualt-cpu	:=st40

bsp-prefix := $(BSP_SRCDIR)/stx7109

ics-objs := \
	admin/admin.o \
	admin/admin_client.o \
	channel/channel.o \
	connect/connect.o \
	cpu/cpu.o \
	debug/debug.o \
	debug/debug_mem.o \
	debug/debug_mmap.o \
	dyn/dyn.o \
	dyn/dyn_client.o \
	elf/elf.o \
	event/event.o \
	heap/heap.o \
	init/ics_init.o \
	linux/ics_module.o \
	linux/ics_module_procfs.o \
	linux/linux.o \
	linux/linux_debug.o \
	linux/linux_event.o \
	linux/linux_task.o \
	load/load.o \
	mailbox/mailbox.o \
	msg/msg_cancel.o \
	msg/msg_recv.o \
	msg/msg_send.o \
	nsrv/nsrv.o \
	nsrv/nsrv_client.o \
	port/port.o \
	region/region.o \
	shm/shm_debug.o \
	shm/shm_init.o \
	shm/shm_channel_alloc.o \
	shm/shm_channel_open.o \
	shm/shm_channel_recv.o \
	shm/shm_channel_send.o \
	shm/shm_connect.o \
	shm/shm_stats.o \
	shm/shm_watchdog.o \
	stats/stats.o \
	transport/transport.o \
	watchdog/watchdog.o \
	$(bsp-prefix)/cores.o \
	$(bsp-prefix)/$(defualt-cpu)/$(bsp-core)/name.o \
	$(bsp-prefix)/$(defualt-cpu)/reset.o \
	$(bsp-prefix)/$(defualt-cpu)/$(bsp-core)/mbox.o \

ics_user-objs := \
	linux/ics_user_module.o \

else

#
# Outside Linux kernel tree
#
PWD	     := $(shell pwd)

V            ?= 0

ARCH         ?= sh

CROSS_COMPILE ?= sh4-linux-

default:
	$(MAKE) V=$(V) ARCH=$(ARCH) CROSS_COMPILE=$(CROSS_COMPILE) -C $(KERNELDIR) O=$(O) SUBDIRS=$(PWD) modules

clean:
	$(MAKE) V=$(V) ARCH=$(ARCH) CROSS_COMPILE=$(CROSS_COMPILE) -C $(KERNELDIR) O=$(O) SUBDIRS=$(PWD) clean

endif
