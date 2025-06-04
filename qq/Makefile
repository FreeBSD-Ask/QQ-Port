PORTNAME=       qq
PORTVERSION=    ${QQ_VER}.${QQ_BUILD}
CATEGORIES=     net-im linux

MASTER_SITES=   https://dldir1.qq.com/qqfile/qq/QQNT/Linux/
DISTNAME=       QQ_${QQ_VER}_${QQ_DATE}_${LINUX_ARCH_${ARCH}}_${QQ_BUILD}
DISTFILES=      ${DISTNAME}.rpm

MAINTAINER=     yklaxds@gmail.com
COMMENT=        Tencent QQ for Linux
WWW=            https://im.qq.com/linuxqq/

USES=           linux:rl9
USE_LINUX=      xorglibs nss dbus cups-libs alsalib alsa-plugins-oss alsa-plugins-pulseaudio ffmpeg-libs

ONLY_FOR_ARCHS= aarch64 amd64

SHEBANG_FILES=  opt/QQ/qq

NO_BUILD=       yes
NO_WRKSUBDIR=   yes

QQ_VER=         3.2.17
QQ_DATE=        250521
QQ_BUILD=       01

# Architecture mapping
LINUX_ARCH_amd64=      x86_64
LINUX_ARCH_aarch64=    aarch64

post-extract:
	@${REINPLACE_CMD} -e 's|^Exec=/opt/QQ/qq %U|Exec=${PREFIX}/share/qq/qq --no-sandbox|' \
		${WRKSRC}/usr/share/applications/qq.desktop

do-install:
	${MKDIR} ${STAGEDIR}${PREFIX}/share/qq
	cd ${WRKDIR}/qq-${QQ_VER}.${QQ_BUILD}/opt/QQ && ${COPYTREE_SHARE} . ${STAGEDIR}${PREFIX}/share/qq
	cd ${WRKSRC}/usr/share && ${COPYTREE_SHARE} . ${STAGEDIR}${PREFIX}/share
	${CHMOD} +x ${STAGEDIR}${PREFIX}/share/qq/qq

.include <bsd.port.mk>
