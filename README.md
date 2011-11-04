# ant-build-common
## Description
A file meant to be included with ant build files that includes the basic targets to build, test, and document Java projects.  It requires no extra libraries, ant extensions, or other crap.

## Usage
Within an ant file (outside of a task) include the following bit:

    <property name="ant-build-common.dir" location="/tmp/ant-build-common"></property>
	<echo message="Importing ant-build-common in ${ant.project.name}."></echo>
	<exec executable="/bin/sh">
	  <arg line='-c "git clone git://github.com/kgilmer/ant-build-common.git ${ant-build-common.dir} 2&gt; /dev/null"'/>
	</exec>	
	<import file="${ant-build-common.dir}/build-common.xml"/>

## Top-level build
When building a product or project that consists of several ant-based projects, a top level ant script can be created that builds each project.

    <project name="project.name">
    	<property name="ant-build-common.dir" location="${basedir}/ant-build-common"></property>
    	<property name="deps" location="${basedir}/deps" />
    	<property name="dist" location="${basedir}/dist" />
    	
    	<!-- task to build all children components of project -->
    	<target name="call-children" description="Call targets on all project components.">
    		<ant dir="component-1" target="${target}"/>
    		<ant dir="component-2" target="${target}"/>			
    	</target>
    	
    	<!-- The following targets set the ${target} variable and run 'call-children'. -->	
    	<target name="clean">
    		<property name="target" value="clean"></property>
    		<antcall target="call-children"></antcall>
    	</target>
    	
    	<target name="clobber">
    		<property name="target" value="clobber"></property>
    		<antcall target="call-children"></antcall>
    		<!-- Delete the common build file -->
    		<delete dir="${ant-build-common.dir}" />
    	</target>
    	
    	<target name="fetch.deps">
    		<property name="target" value="fetch.deps"></property>
    		<antcall target="call-children"></antcall>
    	</target>
    	
    	<target name="compile">
    		<property name="target" value="compile"></property>
    		<antcall target="call-children"></antcall>
    	</target>
    	
    	<target name="jar">
    		<property name="target" value="jar"></property>
    		<antcall target="call-children"></antcall>
    	</target>
    	
    	<target name="javadoc">
    		<property name="target" value="javadoc"></property>
    		<antcall target="call-children"></antcall>
    	</target>
    	
    	<target name="help">
    		<property name="target" value="help"></property>
    		<antcall target="call-children"></antcall>
    	</target>
    </project>
