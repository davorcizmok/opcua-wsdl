# Author: Alexander Rykovanov 2013
#
# Distributed under the GNU LGPL License
# (See accompanying file LICENSE or copy at 
# http://www.gnu.org/licenses/lgpl.html)
#

AC_INIT([opcua-wsdl], [0.1.2], [rykovanov.as@gmail.com])
AC_CONFIG_AUX_DIR([.])
AC_CONFIG_SRCDIR([src/soap_module.cpp])
AM_INIT_AUTOMAKE([-Wall -Werror])

CXXFLAGS="-O0 -g -Wall -std=c++0x"

AC_PROG_CXX
AM_PROG_AR
AC_PROG_LIBTOOL

AC_CONFIG_MACRO_DIR([m4])
AC_CONFIG_HEADER([config.h])

#check headers
AC_CHECK_HEADERS([unistd.h])

PKG_CHECK_MODULES([GSOAP], ["gsoapssl++"])

AC_ARG_WITH([gtest], 
            [AS_HELP_STRING([--with-gtest=DIR], [defines path to gtest root directory])],
            [ 
              AC_SUBST([GTEST_LIB], [-Wl,--whole-archive,$with_gtest/lib/.libs/libgtest.a,--no-whole-archive])
              AC_SUBST([GTEST_MAIN_LIB], [-Wl,--whole-archive,$with_gtest/lib/.libs/libgtest_main.a,--no-whole-archive])
              AC_SUBST([GTEST_INCLUDES], [-I$with_gtest/include])
              AC_MSG_NOTICE([Gtest path: $GTEST_INCLUDES]) 
            ], 
            [ 
              AC_SUBST([GTEST_LIB], [-lgtest])
              AC_SUBST([GTEST_MAIN_LIB], [-lgtest_main])
           ])

AC_ARG_WITH([gmock], 
            [AS_HELP_STRING([--with-gmock=DIR], [defines path to gmock root directory])],
            [ 
              AC_SUBST([GMOCK_LIB], [-Wl,--whole-archive,$with_gmock/lib/.libs/libgmock.a,--no-whole-archive])
              AC_SUBST([GMOCK_INCLUDES], [-I$with_mock/include])
              AC_MSG_NOTICE([gmock path: $GMOCK_INCLUDES]) 
            ], 
            [ 
              AC_SUBST([GMOCK_LIB], [-lgmock])
           ])

AC_ARG_WITH([ua-mappings],
            [AS_HELP_STRING([--with-ua-mappings=DIR], [defines path to ua mappings root directory])],
            [
              AC_SUBST([UA_MAPPING_LIBS], ["-L$with_ua_mappings/.libs -lopcuabinary"])
              AC_SUBST([UA_MAPPING_INCLUDES], [-I$with_ua_mappings/include])
              AC_MSG_NOTICE([ua mappings path: $with_ua_mappings])
            ],
            [
              AC_SUBST([UA_MAPPING_LIBS], ["-lopcuabinary"])
            ])

AC_ARG_WITH([libopccore],
            [AS_HELP_STRING([--with-libopccore=DIR], [defines path to the root directory of libopccore library.])],
            [
              AC_SUBST([OPC_CORE_LIBS], ["-L$with_libopccore/.libs -lopccore -lxml2"])
              AC_SUBST([OPC_CORE_INCLUDES], ["-I$with_libopccore/include -I/usr/include/libxml2"])
              AC_MSG_NOTICE([libopccore path: $with_libopccore])
            ],
            [
              AC_SUBST([OPC_CORE_INCLUDES], ["-I/usr/include/libxml2"])
              AC_SUBST([OPC_CORE_LIBS], ["-lopcuacore -lxml2"])
            ])

AC_ARG_WITH([libopcuaclient],
            [AS_HELP_STRING([--with-libopcuaclient=DIR], [defines path to the root directory of libopcua_client library.])],
            [
              AC_SUBST([OPC_CLIENT_LIBS], ["-L$with_libopcuaclient/.libs -lopcua_client"])
              AC_SUBST([OPC_CLIENT_INCLUDES], [-I$with_libopcuaclient/include])
              AC_MSG_NOTICE([libopcuaclient path: $with_libopcuaclient])
            ],
            [
              AC_SUBST([OPC_CLIENT_LIBS], [-lopcua_client])
            ])

#################################################################
AC_CONFIG_FILES([Makefile])

AC_OUTPUT
