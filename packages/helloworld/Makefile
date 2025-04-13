# helloworld 包的元数据
include $(TOPDIR)/rules.mk

# 包名称、版本等信息
PKG_NAME:=helloworld
PKG_VERSION:=1.0
PKG_RELEASE:=1

# 定义包的基本信息
PKG_MAINTAINER:=Your Name <your@email.com>
PKG_LICENSE:=MIT

# 包含 OpenWrt 的包构建模板
include $(INCLUDE_DIR)/package.mk

# 定义包的配置
define Package/helloworld
    SECTION:=utils
    CATEGORY:=Utilities
    TITLE:=A simple Hello World program
    DEPENDS:=+libc
endef

# 包的描述
define Package/helloworld/description
    This is a minimal example of a custom OpenWrt package.
    Features:
    - Prints "Hello World" to console
    - Demonstrates basic package structure
    - Easy to modify and extend
endef

# 编译逻辑（编译 helloworld.c 为可执行文件）
define Build/Prepare
    mkdir -p $(PKG_BUILD_DIR)
    $(CP) ./src/* $(PKG_BUILD_DIR)/
endef

define Build/Compile
    $(TARGET_CC) $(TARGET_CFLAGS) $(TARGET_LDFLAGS) -Wall -O2 \
        -o $(PKG_BUILD_DIR)/helloworld $(PKG_BUILD_DIR)/helloworld.c
endef

# 安装逻辑（将可执行文件复制到固件中）
define Package/helloworld/install
    $(INSTALL_DIR) $(1)/usr/bin
    $(INSTALL_BIN) $(PKG_BUILD_DIR)/helloworld $(1)/usr/bin/
endef

# 调用 OpenWrt 的包构建宏
$(eval $(call BuildPackage,helloworld))
