pkgname=spirv-tools
pkgver=1.4.321.0
pkgrel=1
pkgdesc="API and commands for processing SPIR-V modules"
arch=('x86_64')
url="https://www.khronos.org/vulkan/"
license=('Apache-2.0')
groups=('vulkan-devel')
depends=(
    'bash'
    'gcc-libs'
    'glibc'
)
makedepends=(
    'cmake'
    'ninja'
    'python'
    'spirv-headers'
)
source=(https://github.com/KhronosGroup/SPIRV-Tools/archive/refs/tags/vulkan-sdk-${pkgver}/SPIRV-Tools-vulkan-sdk-${pkgver}.tar.gz)
sha256sums=(8327fb8f3e9472346a004c91dbb83a6e5f3b36c3846c142cf8c0dc8fac8710f3)

build() {
    cd SPIRV-Tools-vulkan-sdk-${pkgver}

    local cmake_args=(
        -B flarebird-build
        -G Ninja
        -D CMAKE_BUILD_TYPE=Release
        -D CMAKE_INSTALL_PREFIX=/usr
        -D CMAKE_INSTALL_LIBDIR=lib64
        -D CMAKE_INSTALL_SYSCONFDIR=/etc
        -D SPIRV_WERROR=OFF
        -D BUILD_SHARED_LIBS=ON
        -D SPIRV_TOOLS_BUILD_STATIC=OFF
        -D SPIRV-Headers_SOURCE_DIR=/usr
        -D CMAKE_SKIP_INSTALL_RPATH=ON
    )

    cmake "${cmake_args[@]}"

    ninja -C flarebird-build
}

package() {
    cd SPIRV-Tools-vulkan-sdk-${pkgver}

    DESTDIR=${pkgdir} ninja -C flarebird-build install
}
