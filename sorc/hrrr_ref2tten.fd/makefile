# makefile for nssl_porcess
#! /bin/sh -v

# Define the fortran compiler and options

WRFDIR=/gpfs/hps/nco/ops/nwprod/wrf_shared.v1.1.0-intel
FC   = ftn
CC  = 
FLAGS= -assume byterecl
CPPFLAGS = -DLINUX -Dfunder -DFortranByte=char -DFortranInt=int -DFortranLlong='long long' -DNOUNDERSCORE

INCLD= -I${NETCDF}/include  -I${WRFDIR}/inc -I${WRFDIR}/frame # -I${GSIDIR}/include
LIBS = -L${NWPLIBS} \
        $(WRFDIR)/external/io_int/libwrfio_int.a \
        $(WRFDIR)/external/io_netcdf/libwrfio_nf.a \
        $(WRFDIR)/frame/module_machine.o \
        ${WRFDIR}/frame/pack_utils.o \
        -L${NETCDF}/lib \
        -lnetcdf

OBJS = kinds.o constants.o read_netcdf_mass.o BackgroundCld.o pbl_height.o vinterp_radar_ref.o \
       build_missing_REFcone.o radar_ref2tten.o smooth.o convert_stcst2ref.o convert_lghtn2ref.o read_Lightning_cld.o

all: hrrr_ref2tten

hrrr_ref2tten: ${OBJS} gsdcloudanalysis_ref2tten.o
	${FC} -o ../../exec/hrrr_ref2tten ${FLAGS} gsdcloudanalysis_ref2tten.o ${OBJS} ${LIBS} 

.SUFFIXES : .F90 .f90 .f .c .o

.F90.o :
	${FC} ${FLAGS} ${INCLD} -c $<

.f90.o :
	${FC} ${FLAGS} ${INCLD} -c $<

.c.o :
	${CC} ${CPPFLAGS} -c $<

clean:
	/bin/rm -f *.o hrrr_ref2tten *.mod
