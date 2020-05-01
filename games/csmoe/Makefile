# $OpenBSD: Makefile.template,v 1.87 2020/03/22 17:18:01 cwen Exp $

COMMENT =	Cross-platform Counter-Strike mod based on Xash3D

V =	21
DISTNAME =	${V}-lcsm
# PKGNAME defaults to DISTNAME unless changed
PKGNAME =	csmoe-${V}
GIT_HASH_MAINUI =	c819d2f
GIT_COMMIT_MAINUI =	c819d2f59407979af8c27e82430b0541e1709d72
GIT_HASH_GAMEDIR =	9a7b6aa
GIT_COMMIT_GAMEDIR =	9a7b6aae3d119e5d9496c0f529ac42e595a56fde

CATEGORIES =	games

#GPLV3
PERMIT_PACKAGE =	Yes

WANTLIB += ${COMPILER_LIBCXX} c fontconfig freetype m z SDL2

EXTRACT_SUFX =		.tar.gz

MASTER_SITES0 =	https://github.com/MoeMod/CSMoE/archive/
MASTER_SITES1 =	https://github.com/MoeMod/mainui_cpp/archive/
MASTER_SITES2 =	https://github.com/MoeMod/CSMoE-GameDir/archive/
DISTFILES =	v${DISTNAME}${EXTRACT_SUFX}:0 \
		${GIT_HASH_MAINUI}${EXTRACT_SUFX}:1 \
		${GIT_HASH_GAMEDIR}${EXTRACT_SUFX}:2

COMPILER =		base-clang ports-gcc

MODULES =		devel/cmake

LIB_DEPENDS =		devel/sdl2

WRKDIST =		${WRKDIR}/CSMoE-${DISTNAME}

CSMOE_SHARE_DIR =	${PREFIX}/share/csmoe

post-extract:
	cp -R ${WRKDIR}/mainui_cpp-${GIT_COMMIT_MAINUI}/* ${WRKSRC}/mainui_cpp

do-install:
	${INSTALL_PROGRAM} ${WRKBUILD}/game_launch/game_launch ${PREFIX}/bin/csmoe
	${INSTALL_PROGRAM} ${WRKBUILD}/engine/libxash.so ${PREFIX}/lib
	${INSTALL_DATA_DIR} ${CSMOE_SHARE_DIR}
	cp -Rp ${WRKDIR}/CSMoE-GameDir-${GIT_COMMIT_GAMEDIR}/csmoe/* \
			${CSMOE_SHARE_DIR}
	chown -R ${SHAREOWN}:${SHAREGRP} ${CSMOE_SHARE_DIR}/*
	${INSTALL_DATA_DIR} ${CSMOE_SHARE_DIR}/cl_dlls
	${INSTALL_DATA_DIR} ${CSMOE_SHARE_DIR}/dlls
	${INSTALL_PROGRAM} ${WRKBUILD}/cl_dll/client64.so \
			${CSMOE_SHARE_DIR}/cl_dlls
	${INSTALL_PROGRAM} ${WRKBUILD}/mainui_cpp/libxashmenu64.so \
			${CSMOE_SHARE_DIR}/cl_dlls
	${INSTALL_PROGRAM} ${WRKBUILD}/dlls/cs.so \
			${CSMOE_SHARE_DIR}/dlls

.include <bsd.port.mk>
