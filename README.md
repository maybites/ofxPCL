# Setup instruction (OS X)

1. Get dependencies (96.9 MB) and extract them to ofxPCL folder.

		$ curl -O http://structor.jp/dist/ofxpcl_16_libs.zip
		$ unzip ofxpcl_16_libs.zip


1. Change `Project.xcconfig` like

		OFXPCL_PATH = $(OF_PATH)/addons/ofxPCL

		OFXPCL_OTHER_LDFLAGS = -L$(OFXPCL_PATH)/libs/pcl/lib/osx -lpcl_common -lpcl_features -lpcl_filters -lpcl_geometry -lpcl_io -lpcl_io_ply -lpcl_kdtree -lpcl_keypoints -lpcl_octree -lpcl_registration -lpcl_sample_consensus -lpcl_search -lpcl_segmentation -lpcl_surface -lpcl_tracking -lqhull

		OFXPCL_HEADER_SEARCH_PATHS = $(OFXPCL_PATH)/libs/pcl/include/ $(OFXPCL_PATH)/libs/pcl/include/eigen3 $(OFXPCL_PATH)/libs/pcl/include/pcl-1.6

		OFXPCL_LD_RUNPATH_SEARCH_PATHS = @executable_path/../../../../../../../addons/ofxPCL/libs/pcl/lib/osx @executable_path/../../../data/pcl/lib

		LD_RUNPATH_SEARCH_PATHS = $(OFXPCL_LD_RUNPATH_SEARCH_PATHS)

		OTHER_LDFLAGS = $(OF_CORE_LIBS) $(OFXPCL_OTHER_LDFLAGS)
		HEADER_SEARCH_PATHS = $(OF_CORE_HEADERS) $(OFXPCL_HEADER_SEARCH_PATHS)

1. Add ofxPCL/src filder to Xcode project.

1. Copy libraries to data folder

		$ python copyfiles.py PATH_TO_YOUR_PROJECT

1. add a custom build setting of USE_HEADERMAP = NO for the target. 
	1. Open the target's info panel on the "Build" pane.
	2. Pull down the action pop-up menu at the bottom left of the window, select "Add User-Defined Setting".
	3. In the newly added line, set the first column ("Setting") to USE_HEADERMAP, and the second column ("Value") to NO.

1. add the correct include the following paths to the target (target Build settings "Header Search Paths"). In my example that would be:
	1. ../../../addons/ofxPCL/src
	2. ../../../addons/ofxPCL/libs/pcl/include/pcl-1.6
	3. ../../../addons/ofxPCL/libs/pcl/include/eigen3
	4. ../../../addons/ofxPCL/libs/pcl/include

1. Any other additional ofx libraries need to be added in the same fashion.