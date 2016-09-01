# in a bash script you can source this file from /${ILCSOFT} 
#source ITK-EuTelescope/README.md 
#to install EUTelescope using sft available on your local CVMFS installation. 
# tested with LCG_85 
export ILCSOFT=${PWD} 
svn co https://svnsrv.desy.de/public/ilctools/ilcinstall/branches/v01-17-10-eutel-pre/ ilcinstall_v01-17-10-eutel 
#you may need to change this 
source  /cvmfs/sft.cern.ch/lcg/views/LCG_85/x86_64-slc6-gcc49-opt/setup.sh
export G4_DIR=/cvmfs/sft.cern.ch/lcg/releases/Geant4/10.02.p02-1c9b9/x86_64-slc6-gcc49-opt
export G4INSTALL=/cvmfs/sft.cern.ch/lcg/releases/Geant4/10.02.p02-1c9b9/x86_64-slc6-gcc49-opt
ilcinstall_v01-17-10-eutel
#then run the following commands:
patch ilcinstall_v01-17-10-eutel/ilcsoft/ilcsoft.py ITK-EuTelescope/ilcsoft.patch 
patch ilcinstall_v01-17-10-eutel/ilcsoft/eutelescope.py ITK-EuTelescope/eutelescope.patch
patch ilcinstall_v01-17-10-eutel/ilcsoft/marlinutil.py  ITK-EuTelescope/marlinutil.patch
patch ilcinstall_v01-17-10-eutel/releases/v01-17-10/release-base.cfg  ITK-EuTelescope/release-base.patch
patch ilcinstall_v01-17-10-eutel/releases/v01-17-10/release-versions.py  ITK-EuTelescope/release-versions.patch
cp ITK-EuTelescope/externals.patch ilcinstall_v01-17-10-eutel/examples/eutelescope/
cp ITK-EuTelescope/FindG4.patch ilcinstall_v01-17-10-eutel/examples/eutelescope/
cp ITK-EuTelescope/CMakeLists.patch ilcinstall_v01-17-10-eutel/examples/eutelescope/

cp ITK-EuTelescope/release-cvmfs.cfg ilcinstall_v01-17-10-eutel/examples/eutelescope/release-cvmfs.cfg
cd ${ILCSOFT}/ilcinstall_v01-17-10-eutel
./ilcsoft-install -i examples/eutelescope/release-cvmfs.cfg

