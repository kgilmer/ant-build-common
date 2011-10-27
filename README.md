# ant-build-common
## description
A file meant to be included with ant build files that includes the basic targets to build, test, and document Java projects.  It requires no extra libraries, ant extensions, or other crap.

## usage
Within an ant file (outside of a task) include the following bit:

    <exec executable="/usr/bin/git">
    	<arg line="clone" />
    	<arg line="git://github.com/kgilmer/ant-build-common.git" />
    	<arg line="/tmp/ant-build-common" />
    </exec>
    <import file="/tmp/ant-build-common/build-common.xml"/>
