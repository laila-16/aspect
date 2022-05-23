(parameters:Boundary_20velocity_20model)=
# Boundary velocity model


## **Subsection:** Boundary velocity model


(parameters:Boundary_20velocity_20model/Prescribed_20velocity_20boundary_20indicators)=
### __Parameter name:__ Prescribed velocity boundary indicators
**Default value:**

**Pattern:** [Map of <[Anything]>:<[Selection ascii data|function|gplates|zero velocity ]> of length 0...4294967295 (inclusive)]

**Documentation:** A comma separated list denoting those boundaries on which the velocity is prescribed, i.e., where unknown external forces act to prescribe a particular velocity. This is often used to prescribe a velocity that equals that of overlying plates.

The format of valid entries for this parameter is that of a map given as &lsquo;&lsquo;key1 [selector]: value1, key2 [selector]: value2, key3: value3, ...&rsquo;&rsquo; where each key must be a valid boundary indicator (which is either an integer or the symbolic name the geometry model in use may have provided for this part of the boundary) and each value must be one of the currently implemented boundary velocity models. &lsquo;&lsquo;selector&rsquo;&rsquo; is an optional string given as a subset of the letters &lsquo;xyz&rsquo; that allows you to apply the boundary conditions only to the components listed. As an example, &rsquo;1 y: function&rsquo; applies the type &lsquo;function&rsquo; to the y component on boundary 1. Without a selector it will affect all components of the velocity.

Note that the no-slip boundary condition is a special case of the current one where the prescribed velocity happens to be zero. It can thus be implemented by indicating that a particular boundary is part of the ones selected using the current parameter and using &lsquo;&lsquo;zero velocity&rsquo;&rsquo; as the boundary values. Alternatively, you can simply list the part of the boundary on which the velocity is to be zero with the parameter &lsquo;&lsquo;Zero velocity boundary indicator&rsquo;&rsquo; in the current parameter section.

Note that when &lsquo;&lsquo;Use years in output instead of seconds&rsquo;&rsquo; is set to true, velocity should be given in m/yr. The following boundary velocity models are available:

&lsquo;ascii data&rsquo;: Implementation of a model in which the boundary velocity is derived from files containing data in ascii format. Note the required format of the input data: The first lines may contain any number of comments if they begin with &lsquo;#&rsquo;, but one of these lines needs to contain the number of grid points in each dimension as for example &lsquo;# POINTS: 3 3&rsquo;. The order of the data columns has to be &lsquo;x&rsquo;, &lsquo;velocity${}_x$&rsquo;, &lsquo;velocity${}_y$&rsquo; in a 2d model or &lsquo;x&rsquo;, &lsquo;y&rsquo;, &lsquo;velocity${}_x$&rsquo;, &lsquo;velocity${}_y$&rsquo;, &lsquo;velocity${}_z$&rsquo; in a 3d model. Note that the data in the input files need to be sorted in a specific order: the first coordinate needs to ascend first, followed by the second in order to assign the correct data to the prescribed coordinates.If you use a spherical model, then the assumed grid changes. &lsquo;x&rsquo; will be replaced by the radial distance of the point to the bottom of the model, &lsquo;y&rsquo; by the azimuth angle and &lsquo;z&rsquo; by the polar angle measured positive from the north pole. The grid will be assumed to be a latitude-longitude grid. Note that the order of spherical coordinates is &lsquo;r&rsquo;, &lsquo;phi&rsquo;, &lsquo;theta&rsquo; and not &lsquo;r&rsquo;, &lsquo;theta&rsquo;, &lsquo;phi&rsquo;, since this allows for dimension independent expressions. Velocities can be specified using cartesian (by default) or spherical unit vectors. No matter which geometry model is chosen, the unit of the velocities is assumed to be m/s or m/yr depending on the &lsquo;Use years in output instead of seconds&rsquo; flag. If you provide velocities in cm/yr, set the &lsquo;Scale factor&rsquo; option to 0.01.

&lsquo;function&rsquo;: Implementation of a model in which the boundary velocity is given in terms of an explicit formula that is elaborated in the parameters in section &lsquo;&lsquo;Boundary velocity model|Function&rsquo;&rsquo;. The format of these functions follows the syntax understood by the muparser library, see Section~\ref{sec:muparser-format}.

The formula you describe in the mentioned section is a semicolon separated list of velocities for each of the $d$ components of the velocity vector. These $d$ formulas are interpreted as having units m/s, unless the global input parameter &lsquo;&lsquo;Use years in output instead of seconds&rsquo;&rsquo; is set, in which case we interpret the formula expressions as having units m/year.

Likewise, since the symbol $t$ indicating time may appear in the formulas for the prescribed velocities, it is interpreted as having units seconds unless the global parameter above has been set.

&lsquo;gplates&rsquo;: Implementation of a model in which the boundary velocity is derived from files that are generated by the GPlates program.

&lsquo;zero velocity&rsquo;: Implementation of a model in which the boundary velocity is zero. This is commonly referred to as a &lsquo;&lsquo;stick boundary condition&rsquo;&rsquo;, indicating that the material &lsquo;&lsquo;sticks&rsquo;&rsquo; to the material on the other side of the boundary.

(parameters:Boundary_20velocity_20model/Tangential_20velocity_20boundary_20indicators)=
### __Parameter name:__ Tangential velocity boundary indicators
**Default value:**

**Pattern:** [List of <[Anything]> of length 0...4294967295 (inclusive)]

**Documentation:** A comma separated list of names denoting those boundaries on which the velocity is tangential and unrestrained, i.e., free-slip where no external forces act to prescribe a particular tangential velocity (although there is a force that requires the flow to be tangential).

The names of the boundaries listed here can either by numbers (in which case they correspond to the numerical boundary indicators assigned by the geometry object), or they can correspond to any of the symbolic names the geometry object may have provided for each part of the boundary. You may want to compare this with the documentation of the geometry model you use in your model.

(parameters:Boundary_20velocity_20model/Zero_20velocity_20boundary_20indicators)=
### __Parameter name:__ Zero velocity boundary indicators
**Default value:**

**Pattern:** [List of <[Anything]> of length 0...4294967295 (inclusive)]

**Documentation:** A comma separated list of names denoting those boundaries on which the velocity is zero.

The names of the boundaries listed here can either by numbers (in which case they correspond to the numerical boundary indicators assigned by the geometry object), or they can correspond to any of the symbolic names the geometry object may have provided for each part of the boundary. You may want to compare this with the documentation of the geometry model you use in your model.

(parameters:Boundary_20velocity_20model/Ascii_20data_20model)=
## **Subsection:** Boundary velocity model / Ascii data model
(parameters:Boundary_20velocity_20model/Ascii_20data_20model/Data_20directory)=
### __Parameter name:__ Data directory
**Default value:** $ASPECT_SOURCE_DIR/data/boundary-velocity/ascii-data/test/

**Pattern:** [DirectoryName]

**Documentation:** The name of a directory that contains the model data. This path may either be absolute (if starting with a &lsquo;/&rsquo;) or relative to the current directory. The path may also include the special text &lsquo;$ASPECT_SOURCE_DIR&rsquo; which will be interpreted as the path in which the ASPECT source files were located when ASPECT was compiled. This interpretation allows, for example, to reference files located in the &lsquo;data/&rsquo; subdirectory of ASPECT.

(parameters:Boundary_20velocity_20model/Ascii_20data_20model/Data_20file_20name)=
### __Parameter name:__ Data file name
**Default value:** box_2d_%s.%d.txt

**Pattern:** [Anything]

**Documentation:** The file name of the model data. Provide file in format: (File name).\%s\%d, where \%s is a string specifying the boundary of the model according to the names of the boundary indicators (of the chosen geometry model), and \%d is any sprintf integer qualifier specifying the format of the current file number.

(parameters:Boundary_20velocity_20model/Ascii_20data_20model/Data_20file_20time_20step)=
### __Parameter name:__ Data file time step
**Default value:** 1e6

**Pattern:** [Double 0...MAX_DOUBLE (inclusive)]

**Documentation:** Time step between following data files. Depending on the setting of the global &lsquo;Use years in output instead of seconds&rsquo; flag in the input file, this number is either interpreted as seconds or as years. The default is one million, i.e., either one million seconds or one million years.

(parameters:Boundary_20velocity_20model/Ascii_20data_20model/Decreasing_20file_20order)=
### __Parameter name:__ Decreasing file order
**Default value:** false

**Pattern:** [Bool]

**Documentation:** In some cases the boundary files are not numbered in increasing but in decreasing order (e.g. &lsquo;Ma BP&rsquo;). If this flag is set to &lsquo;True&rsquo; the plugin will first load the file with the number &lsquo;First data file number&rsquo; and decrease the file number during the model run.

(parameters:Boundary_20velocity_20model/Ascii_20data_20model/First_20data_20file_20model_20time)=
### __Parameter name:__ First data file model time
**Default value:** 0

**Pattern:** [Double 0...MAX_DOUBLE (inclusive)]

**Documentation:** The &lsquo;First data file model time&rsquo; parameter has been deactivated and will be removed in a future release. Do not use this paramter and instead provide data files starting from the model start time.

(parameters:Boundary_20velocity_20model/Ascii_20data_20model/First_20data_20file_20number)=
### __Parameter name:__ First data file number
**Default value:** 0

**Pattern:** [Integer range -2147483648...2147483647 (inclusive)]

**Documentation:** Number of the first velocity file to be loaded when the model time is larger than &lsquo;First velocity file model time&rsquo;.

(parameters:Boundary_20velocity_20model/Ascii_20data_20model/Scale_20factor)=
### __Parameter name:__ Scale factor
**Default value:** 1.

**Pattern:** [Double -MAX_DOUBLE...MAX_DOUBLE (inclusive)]

**Documentation:** Scalar factor, which is applied to the model data. You might want to use this to scale the input to a reference model. Another way to use this factor is to convert units of the input files. For instance, if you provide velocities in cm/yr set this factor to 0.01.

(parameters:Boundary_20velocity_20model/Ascii_20data_20model/Use_20spherical_20unit_20vectors)=
### __Parameter name:__ Use spherical unit vectors
**Default value:** false

**Pattern:** [Bool]

**Documentation:** Specify velocity as r, phi, and theta components instead of x, y, and z. Positive velocities point up, east, and north (in 3D) or out and clockwise (in 2D). This setting only makes sense for spherical geometries.

(parameters:Boundary_20velocity_20model/Function)=
## **Subsection:** Boundary velocity model / Function
(parameters:Boundary_20velocity_20model/Function/Coordinate_20system)=
### __Parameter name:__ Coordinate system
**Default value:** cartesian

**Pattern:** [Selection cartesian|spherical|depth ]

**Documentation:** A selection that determines the assumed coordinate system for the function variables. Allowed values are &lsquo;cartesian&rsquo;, &lsquo;spherical&rsquo;, and &lsquo;depth&rsquo;. &lsquo;spherical&rsquo; coordinates are interpreted as r,phi or r,phi,theta in 2D/3D respectively with theta being the polar angle. &lsquo;depth&rsquo; will create a function, in which only the first parameter is non-zero, which is interpreted to be the depth of the point.

(parameters:Boundary_20velocity_20model/Function/Function_20constants)=
### __Parameter name:__ Function constants
**Default value:**

**Pattern:** [Anything]

**Documentation:** Sometimes it is convenient to use symbolic constants in the expression that describes the function, rather than having to use its numeric value everywhere the constant appears. These values can be defined using this parameter, in the form &lsquo;var1=value1, var2=value2, ...&rsquo;.

A typical example would be to set this runtime parameter to &lsquo;pi=3.1415926536&rsquo; and then use &lsquo;pi&rsquo; in the expression of the actual formula. (That said, for convenience this class actually defines both &lsquo;pi&rsquo; and &lsquo;Pi&rsquo; by default, but you get the idea.)

(parameters:Boundary_20velocity_20model/Function/Function_20expression)=
### __Parameter name:__ Function expression
**Default value:** 0; 0

**Pattern:** [Anything]

**Documentation:** The formula that denotes the function you want to evaluate for particular values of the independent variables. This expression may contain any of the usual operations such as addition or multiplication, as well as all of the common functions such as &lsquo;sin&rsquo; or &lsquo;cos&rsquo;. In addition, it may contain expressions like &lsquo;if(x>0, 1, -1)&rsquo; where the expression evaluates to the second argument if the first argument is true, and to the third argument otherwise. For a full overview of possible expressions accepted see the documentation of the muparser library at http://muparser.beltoforion.de/.

If the function you are describing represents a vector-valued function with multiple components, then separate the expressions for individual components by a semicolon.

(parameters:Boundary_20velocity_20model/Function/Use_20spherical_20unit_20vectors)=
### __Parameter name:__ Use spherical unit vectors
**Default value:** false

**Pattern:** [Bool]

**Documentation:** Specify velocity as $r$, $\phi$, and $\theta$ components instead of $x$, $y$, and $z$. Positive velocities point up, east, and north (in 3D) or out and clockwise (in 2D). This setting only makes sense for spherical geometries.

(parameters:Boundary_20velocity_20model/Function/Variable_20names)=
### __Parameter name:__ Variable names
**Default value:** x,y,t

**Pattern:** [Anything]

**Documentation:** The names of the variables as they will be used in the function, separated by commas. By default, the names of variables at which the function will be evaluated are &lsquo;x&rsquo; (in 1d), &lsquo;x,y&rsquo; (in 2d) or &lsquo;x,y,z&rsquo; (in 3d) for spatial coordinates and &lsquo;t&rsquo; for time. You can then use these variable names in your function expression and they will be replaced by the values of these variables at which the function is currently evaluated. However, you can also choose a different set of names for the independent variables at which to evaluate your function expression. For example, if you work in spherical coordinates, you may wish to set this input parameter to &lsquo;r,phi,theta,t&rsquo; and then use these variable names in your function expression.

(parameters:Boundary_20velocity_20model/GPlates_20model)=
## **Subsection:** Boundary velocity model / GPlates model
(parameters:Boundary_20velocity_20model/GPlates_20model/Data_20directory)=
### __Parameter name:__ Data directory
**Default value:** $ASPECT_SOURCE_DIR/data/boundary-velocity/gplates/

**Pattern:** [DirectoryName]

**Documentation:** The name of a directory that contains the model data. This path may either be absolute (if starting with a &rsquo;/&rsquo;) or relative to the current directory. The path may also include the special text &rsquo;$ASPECT_SOURCE_DIR&rsquo; which will be interpreted as the path in which the ASPECT source files were located when ASPECT was compiled. This interpretation allows, for example, to reference files located in the &lsquo;data/&rsquo; subdirectory of ASPECT.

(parameters:Boundary_20velocity_20model/GPlates_20model/Data_20file_20time_20step)=
### __Parameter name:__ Data file time step
**Default value:** 1e6

**Pattern:** [Double 0...MAX_DOUBLE (inclusive)]

**Documentation:** Time step between following velocity files. Depending on the setting of the global &rsquo;Use years in output instead of seconds&rsquo; flag in the input file, this number is either interpreted as seconds or as years. The default is one million, i.e., either one million seconds or one million years.

(parameters:Boundary_20velocity_20model/GPlates_20model/Decreasing_20file_20order)=
### __Parameter name:__ Decreasing file order
**Default value:** false

**Pattern:** [Bool]

**Documentation:** In some cases the boundary files are not numbered in increasing but in decreasing order (e.g. &rsquo;Ma BP&rsquo;). If this flag is set to &rsquo;True&rsquo; the plugin will first load the file with the number &rsquo;First velocity file number&rsquo; and decrease the file number during the model run.

(parameters:Boundary_20velocity_20model/GPlates_20model/First_20data_20file_20model_20time)=
### __Parameter name:__ First data file model time
**Default value:** 0.

**Pattern:** [Double 0...MAX_DOUBLE (inclusive)]

**Documentation:** Time from which on the velocity file with number &rsquo;First velocity file number&rsquo; is used as boundary condition. Previous to this time, a no-slip boundary condition is assumed. Depending on the setting of the global &rsquo;Use years in output instead of seconds&rsquo; flag in the input file, this number is either interpreted as seconds or as years.

(parameters:Boundary_20velocity_20model/GPlates_20model/First_20data_20file_20number)=
### __Parameter name:__ First data file number
**Default value:** 0

**Pattern:** [Integer range -2147483648...2147483647 (inclusive)]

**Documentation:** Number of the first velocity file to be loaded when the model time is larger than &rsquo;First velocity file model time&rsquo;.

(parameters:Boundary_20velocity_20model/GPlates_20model/Lithosphere_20thickness)=
### __Parameter name:__ Lithosphere thickness
**Default value:** 100000.

**Pattern:** [Double 0...MAX_DOUBLE (inclusive)]

**Documentation:** Determines the depth of the lithosphere, so that the GPlates velocities can be applied at the sides of the model as well as at the surface.

(parameters:Boundary_20velocity_20model/GPlates_20model/Point_20one)=
### __Parameter name:__ Point one
**Default value:** 1.570796,0.0

**Pattern:** [Anything]

**Documentation:** Point that determines the plane in which a 2D model lies in. Has to be in the format &lsquo;a,b&rsquo; where a and b are theta (polar angle) and phi in radians. This value is not utilized in 3D geometries, and can therefore be set to the default or any user-defined quantity.

(parameters:Boundary_20velocity_20model/GPlates_20model/Point_20two)=
### __Parameter name:__ Point two
**Default value:** 1.570796,1.570796

**Pattern:** [Anything]

**Documentation:** Point that determines the plane in which a 2D model lies in. Has to be in the format &lsquo;a,b&rsquo; where a and b are theta (polar angle) and phi in radians. This value is not utilized in 3D geometries, and can therefore be set to the default or any user-defined quantity.

(parameters:Boundary_20velocity_20model/GPlates_20model/Scale_20factor)=
### __Parameter name:__ Scale factor
**Default value:** 1.

**Pattern:** [Double -MAX_DOUBLE...MAX_DOUBLE (inclusive)]

**Documentation:** Scalar factor, which is applied to the boundary velocity. You might want to use this to scale the velocities to a reference model (e.g. with free-slip boundary) or another plate reconstruction.

(parameters:Boundary_20velocity_20model/GPlates_20model/Velocity_20file_20name)=
### __Parameter name:__ Velocity file name
**Default value:** phi.%d

**Pattern:** [Anything]

**Documentation:** The file name of the material data. Provide file in format: (Velocity file name).\%d.gpml where \%d is any sprintf integer qualifier, specifying the format of the current file number.