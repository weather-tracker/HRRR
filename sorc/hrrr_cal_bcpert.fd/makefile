# makefile for boundary perturbation
#! /bin/sh -v

# Define the fortran compiler and options

FC       = ftn
CPP      = /lib/cpp -P
ARCH     =
CPPFLAGS =  -DLINUX -Dfunder -DFortranByte=char -DFortranInt=int -DFortranLlong='long long' -D_UNDERSCORE

INCLD = -I${NETCDF}/include
LIBS =  ${NETCDF}/lib/libnetcdff.a ${NETCDF}/lib/libnetcdf.a  \
        ${HDF5}/lib/libhdf5hl_fortran.a ${HDF5}/lib/libhdf5_hl.a ${HDF5}/lib/libhdf5_fortran.a ${HDF5}/lib/libhdf5.a /usr/lib64/libz.a

OBJS = 

all: hrrr_cal_bcpert

hrrr_cal_bcpert: ${OBJS} hrrre_bc_pert.o
	${FC} -o ../../exec/hrrr_cal_bcpert ${FLAGS} hrrre_bc_pert.o ${OBJS} ${LIBS} 

.SUFFIXES : .F90 .f90 .f .c .o

.F90.o :
	${FC} ${FLAGS} ${INCLD} -c $<

.f90.o :
	${FC} ${FLAGS} ${INCLD} -c $<

.c.o :
	${CC} ${CPPFLAGS} -c $<

clean:
	/bin/rm -f *.o *.exe *.mod hrrr_cal_bcpert
