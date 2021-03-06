# Created by: jseger@FreeBSD.org
# $FreeBSD$

PORTNAME=	cfengine
PORTVERSION=	2.2.10
PORTREVISION=	4
CATEGORIES=	sysutils
MASTER_SITES=	https://s3.amazonaws.com/cfengine.package-repos/tarballs/
PKGNAMESUFFIX=	22

MAINTAINER=	cy@FreeBSD.org
#		gjb@FreeBSD.org is also committer for this port
#		skreuzer@FreeBSD.org is also committer for this port
COMMENT=	Systems administration tool for networks
CPE_VENDOR=	gnu

DEPRECATED=	No longeer supported by cfengine.com
EXPIRATION_DATE=	2018-12-31

FETCH_BEFORE_ARGS=	-o ${DISTDIR}/${DISTFILES}

CONFLICTS=	cfengine-3* cfengine-devel-* cfengine3*

USE_RC_SUBR=	cfexecd cfservd

USES=		bdb cpe libtool makeinfo shebangfix ssl
SHEBANG_FILES=	contrib/cfdoc

GNU_CONFIGURE=	yes
CONFIGURE_ARGS=	--with-docs \
		--docdir=${DOCSDIR} \
		--htmldir=${DOCSDIR}/html
CONFIGURE_ENV+=	BERKELEY_DB_CFLAGS=-I${BDB_INCLUDE_DIR} \
		BERKELEY_DB_LDFLAGS=-L${BDB_LIB_DIR} \
		BERKELEY_DB_LIB=-l${BDB_LIB_NAME}

INFO=		cfengine-Tutorial cfengine-Reference

OPTIONS_DEFINE=	DOCS EXAMPLES

post-patch:
		@${REINPLACE_CMD} -e '/^docdir/s!=.*!= @docdir@!'\
				  ${WRKSRC}/doc/Makefile.in \
				  ${WRKSRC}/Makefile.in
		@${REINPLACE_CMD} -e '/^htmldir/s!=.*!= @htmldir@!'\
				  ${WRKSRC}/doc/Makefile.in \
				  ${WRKSRC}/Makefile.in
		@${REINPLACE_CMD} -e '/^pkgdatadir/s!=.*!= ${EXAMPLESDIR}!'\
				  ${WRKSRC}/inputs/Makefile.in \
				  ${WRKSRC}/contrib/Makefile.in

.include <bsd.port.pre.mk>

.if ${SSL_DEFAULT} != "openssl"
BROKEN_FreeBSD_12=	fails to build with openssl111, install security/openssl
BROKEN_FreeBSD_13=	fails to build with openssl111, install security/openssl
.endif

.include <bsd.port.post.mk>
