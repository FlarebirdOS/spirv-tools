pkgname=spirv-tools
pkgver=1.4.328.1
pkgrel=3
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
    'git'
    'ninja'
    'python'
    'spirv-headers'
)
source=(git+ssh://git@github.com/KhronosGroup/SPIRV-Tools#tag=vulkan-sdk-${pkgver})
sha256sums=(8915a45df7806a9a1ee4eabe6af2eab6621f1de1b5da831b1679de52d86115d6)

build() {
    cd SPIRV-Tools

    local cmake_args=(
        -B flarebird-build
        -G Ninja
        -D CMAKE_BUILD_TYPE=Release
        -D CMAKE_INSTALL_PREFIX=/usr
        -D CMAKE_INSTALL_LIBDIR=lib64
        -D CMAKE_INSTALL_SYSCONFDIR=/etc
        -D CMAKE_SKIP_INSTALL_RPATH=ON
        -D SPIRV-Headers_SOURCE_DIR=/usr
        -D SPIRV_TOOLS_BUILD_STATIC=OFF
        -D SPIRV_WERROR=OFF
        -D BUILD_SHARED_LIBS=ON
    )

    cmake "${cmake_args[@]}"

    ninja -C flarebird-build
}

package() {
    cd SPIRV-Tools

    DESTDIR=${pkgdir} ninja -C flarebird-build install
}
