include $(TOPDIR)/rules.mk

PKG_NAME:=helloworld-rust
PKG_VERSION:=0.1.0
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

# Rust target triple
RUST_TARGET := $(ARCH)-unknown-linux-musl

# Package metadata
PKG_MAINTAINER:=Your Name <your@email.com>
PKG_LICENSE:=MIT

# Rust toolchain dependencies
define Package/helloworld-rust/config
	select PACKAGE_rustc
	select PACKAGE_cargo
endef

define Package/helloworld-rust
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=Rust Hello World
	DEPENDS:=+libc +libstdcpp
endef

define Package/helloworld-rust/description
	This is a minimal Rust example for OpenWrt.
	Features:
	- Demonstrates Rust package integration
	- Shows cross-compilation setup
	- Includes proper stripping
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./src/* $(PKG_BUILD_DIR)/
endef

define Build/Compile
	cd $(PKG_BUILD_DIR) && \
	cargo build --release --target=$(RUST_TARGET) && \
	$(STRIP) $(PKG_BUILD_DIR)/target/$(RUST_TARGET)/release/helloworld-rust
endef

define Package/helloworld-rust/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/target/$(RUST_TARGET)/release/helloworld-rust $(1)/usr/bin/
endef
