MoBeE README

Building MoBeE

1. Install the dependencies:
	- YARP (http://wiki.icub.org/yarp/)
	- Qt (http://qt-project.org/)
	- SOLID (http://www.dtecta.com/)
NOTE: The open-source version of SOLID is a little tricky to find, so I have included it in the MoBeE distribution. Also note that SOLID's examples rely on GLUT, however in my experience SOLID's 'configure' script is not very good at finding it. If you have problems, simply do not compile the examples.

2. Compile MoBeE with the Kinematic Model Demo…
cd someplaceOnYourSystem/MoBeE
mkdir build
cd build
cmake ..
make install

NOTE: here, make install will put all the build results, in someplaceOnYourSystem/MoBeEe/bin, someplaceOnYourSystem/MoBeEe/lib, etc.  Also, you can build MoBeE and/or the kinematic model (which does not depend on YARP) separately by doing the above in someplaceOnYourSystem/MoBeE/src/Apps/MoBeE and/or someplaceOnYourSystem/MoBeE/src/Apps/KinematicModelDemo.

3. Run MoBeE
	- Start a YARP server and an iCub Simulator on a separate machine on your network.
	- Make sure your MoBeE machine can see it with 'yarp where,'
	- If not, use 'yarp detect --write' and/or 'yarp conf 192.168.X.Y 10000'
	- from someplaceOnYourSystem/MoBeEe/bin do:
		./MoBeE --visualize --robot ../xml/icubSim.xml --conf ../ctrlConf/

XML NOTE: The xml file specifies the kinematic/geometric robot model, and also contains the name of the YARP robot who's motor encoder streams should drive it. icubSim.xml looks for a robot named 'icubSim'. If your simulator is named differently, you must edit the beginning of icubSim.xml accordingly. icub.xml is identical to icubSim.xml except that it looks for the real robot, 'icub' instead of 'icubSim'. 

CONF NOTE: The directory someplaceOnYourSystem/MoBeE/ctrlConf contains several files, which define parameters related to the MoBeE controller's internal dynamics. How to tune these is beyond the scope of the README, however to turn off control for a body part, simply rename the appropriate file, such that MoBeE doesn't find it. for example 'head.ini' could be renamed '_head.ini'

4. Play with MoBeE

in someplaceOnYourSystem/MoBeE/bin check out:
	- poses… demonstrates randomized position control for both arms and the torso.
	- circle… demonstrates a simple feed forward operational space control using one arm
	- reaches… demonstrates a more complex feedback operational space control using one arm

also try loading a world configuration from xml, like: 
	./MoBeE --visualize --robot ../xml/icubSim.xml --conf ../ctrlConf/ --world ../xml/world.xml

then try interacting with MoBeE's world online via RPC by running:
	- yarp rpc /MoBeE/world
	- help
	