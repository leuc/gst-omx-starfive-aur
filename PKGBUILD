# Maintainer: Leuc
pkgname=gst-omx-starfive
pkgver=1.22.5
pkgrel=1
pkgdesc="Gstreamer OMX Plugin with StarFive Vision Five 2 SBC patches"
arch=('riscv64')
url="https://github.com/starfive-tech/Debian/tree/20221225T084846Z/multimedia/patch/gstreamer1/sf-gst-omx"
license=('LGPL')
depends=(omx-il)
makedepends=(meson)
provides=(libgstomx.so)
conflicts=(gst-omx)
source=(
  "https://gstreamer.freedesktop.org/src/gst-omx/gst-omx-$pkgver.tar.xz"
  "https://github.com/starfive-tech/Debian/raw/20221225T084846Z/multimedia/patch/gstreamer1/sf-gst-omx/0001-add-starfive-support.patch"
  "https://github.com/starfive-tech/Debian/raw/20221225T084846Z/multimedia/patch/gstreamer1/sf-gst-omx/0002-Fix-gst-omx-Enable-the-gst-omx-VPU-decoding-and-enco.patch"
  "https://github.com/starfive-tech/Debian/raw/20221225T084846Z/multimedia/patch/gstreamer1/sf-gst-omx/0003-add-video-scale-support.patch"
  "https://github.com/starfive-tech/Debian/raw/20221225T084846Z/multimedia/patch/gstreamer1/sf-gst-omx/0004-add-encoder-support.patch"
  "https://github.com/starfive-tech/Debian/raw/20221225T084846Z/multimedia/patch/gstreamer1/sf-gst-omx/0005-rank-257-for-sf-codecs.patch"
  "https://github.com/starfive-tech/Debian/raw/20221225T084846Z/multimedia/patch/gstreamer1/sf-gst-omx/0006-dont-invoke-USE_BUFFER-if-no-dmabuffer.patch"
  "https://github.com/starfive-tech/Debian/raw/20221225T084846Z/multimedia/patch/gstreamer1/sf-gst-omx/0007-add-omxmjpegdec-support.patch"
  "https://github.com/starfive-tech/Debian/raw/20221225T084846Z/multimedia/patch/gstreamer1/sf-gst-omx/0008-support-nv21-i422-y444-for-omxmjpegdec.patch"
  "https://github.com/starfive-tech/Debian/raw/20221225T084846Z/multimedia/patch/gstreamer1/sf-gst-omx/0009-suport-usebuffer-mode-for-encoding.patch"
  "https://github.com/starfive-tech/Debian/raw/20221225T084846Z/multimedia/patch/gstreamer1/sf-gst-omx/0010-add-property-framerate.patch"
  "https://github.com/starfive-tech/Debian/raw/20221225T084846Z/multimedia/patch/gstreamer1/sf-gst-omx/0011-hanle-some-extra-profile-for-avc.patch"
  "https://github.com/starfive-tech/Debian/raw/20221225T084846Z/multimedia/patch/gstreamer1/sf-gst-omx/0012-combine-sps-pps-header-to-idr.patch"
  "https://github.com/starfive-tech/Debian/raw/20221225T084846Z/multimedia/patch/gstreamer1/sf-gst-omx/0013-Modify-sf-component-name-to-in-std-format.patch"
  "https://github.com/starfive-tech/Debian/raw/20221225T084846Z/multimedia/patch/gstreamer1/sf-gst-omx/0014-support-nv21-for-omxh264_5dec.patch"
  "https://github.com/starfive-tech/Debian/raw/20221225T084846Z/multimedia/patch/gstreamer1/sf-gst-omx/0015_Add_NV21_for_gstomxvideoenc_class.patch"
  "https://github.com/starfive-tech/Debian/raw/20221225T084846Z/multimedia/patch/gstreamer1/sf-gst-omx/0016-Modify-gstomxmjpegdec-format.patch"
  "https://github.com/starfive-tech/Debian/raw/20221225T084846Z/multimedia/patch/gstreamer1/sf-gst-omx/0017-support-mirror-rotation-scale-for-gstomxmjpegdec.patch"
  "https://github.com/starfive-tech/Debian/raw/20221225T084846Z/multimedia/patch/gstreamer1/sf-gst-omx/0018-support-cut-for-gstomxmjpegdec.patch"
  "https://github.com/starfive-tech/Debian/raw/20221225T084846Z/multimedia/patch/gstreamer1/sf-gst-omx/0019-Add-Interlaced-mode-judgment.patch"
)
md5sums=(
  343d1dc08cce08c47d1e0ea7df18a419
  726d804e96d610081e99e1d7160b99d4
  560ed5fc0d29b570873adb9e829aa677
  89e8e1db9ede6996a094a460d4cb9309
  db65274074c164e3ed398850fbac5233
  9deecba29c78ba1b3d2d9ae712f10eb4
  61b1107ca6ee0c738fffe9bab9fbf037
  ad90353dba0c109d52bdc7854e3a67e6
  d322a70d40741343ca2306565b73a41d
  84615c74068acd47e9a61c34e43a0184
  eee6a2d5cc668f45038721de4b19872e
  31fe467b554ae7207498dda9bd21a168
  ffb45fba99ac55a86523c867c82f1b26
  b8bb3fff5da3b88a214f70c37f690499
  225b48477c39c6be0f8c2c3b64f1715f
  72cc7506221ec246ba3870d247a9e8fe
  afcd274a16649c6805b46c7946856de8
  eac33de0dc8b09aa4cbeaae941801273
  f4c3b044aa71dfca98bbfc9c8649c4d1
  484544e218123c0b485e3f6f91ba74e8
)

prepare() {
  local _patchfile
  for _patchfile in ${srcdir}/*.patch; do
    patch --quiet --get=0 --strip=1 --remove-empty-files --no-backup-if-mismatch --batch --forward --directory="$srcdir/gst-omx-$pkgver" --input="$_patchfile"
  done
}

build() {
  arch-meson gst-omx-$pkgver build -Dtarget=stf -Dheader_path=/usr/include/omx-il -Ddoc=disabled -Dexamples=disabled
  meson compile -C build
}

package() {
  meson install -C build --destdir "$pkgdir"
}

# vim:set sw=2 ts=2 et:
