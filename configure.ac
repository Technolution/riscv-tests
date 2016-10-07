AC_INIT(riscv-tests, 1.0)

cross_compiling=yes
AC_PROG_CC
AC_PROG_GREP

AC_ARG_WITH(xlen,
        [AS_HELP_STRING([--with-xlen=XLEN],
                [Set XLEN, the X-register bit width (default is 64)])],
        AC_SUBST(XLEN, $withval),
        AC_SUBST(XLEN, 64)
        )
        
##################################
## parse architecture to compile only what the compiler supports
##################################
        
        
AC_DEFUN([MATCH_PATTERN], [echo "$1" | $GREP -qE "$2"])

AC_DEFUN([GENERATE_EXTENSION],
    [AS_IF([MATCH_PATTERN([$1], [^RV(32|64).*$2])],
        AC_SUBST($3, yes),
        AC_SUBST($3, no))]
    )

AC_DEFUN([PARSE_EXTENSIONS],
    [GENERATE_EXTENSION([$1], C, ENABLE_RVC)
     GENERATE_EXTENSION([$1], M, ENABLE_MULT)
     GENERATE_EXTENSION([$1], A, ENABLE_ATOMIC)
     GENERATE_EXTENSION([$1], F, ENABLE_FLOAT)
     GENERATE_EXTENSION([$1], D, ENABLE_DOUBLE)]
    )

AC_DEFUN([PARSE_BASE_ARCH],
    [AS_IF([MATCH_PATTERN([$1], [^RV32])],
        AC_SUBST(XLEN, 32))
    AS_IF([MATCH_PATTERN([$1], [^RV64])],
        AC_SUBST(XLEN, 64))]
    )

AC_ARG_WITH(arch,
    [AS_HELP_STRING([--with-arch=RV64IMAFD],
        [Sets the base RISC-V ISA, defaults to RV64IMAFD])],
    [PARSE_BASE_ARCH([$withval])
     PARSE_EXTENSIONS([$withval])
     AC_SUBST(ARCH, $withval)],
    []
    )
        

AC_OUTPUT(
    Makefile
)
