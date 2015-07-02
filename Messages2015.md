# Messages 2015
----
Autor: Florian Gehrig  
Klasse: HF2A  
Datum: 30. Juni 2015  
Version: 1.0  

----
- <a href="#SM1">AttentionMessages</a>
- <a href="#SM2">BeaconSignal</a>
- <a href="#SM3">ExplorationInfo</a>
- <a href="#SM4">GameInfo</a>
- <a href="#SM5">GameState</a>
- <a href="#SM6">MachineCommands</a>
- <a href="#SM7">MachineInfo</a>
- <a href="#SM8">MachineInstructions</a>
- <a href="#SM9">MachineReport</a>
- <a href="#SM10">OrderInfo</a>
- <a href="#SM11">Pose2D</a>
- <a href="#SM12">ProductColor</a>
- <a href="#SM13">RingInfo</a>
- <a href="#SM14">RobotCommand</a>
- <a href="#SM15">RobotInfo</a>
- <a href="#SM16">SimTimeSync</a>
- <a href="#SM17">Team</a>
- <a href="#SM18">Time</a>
- <a href="#SM19">VersionInfo</a>
- <a href="#SM20">Zone</a>

----
# <a name="SM1">AttentionMessages</a>
	package llsf_msgs;
	
	import "Team.proto";
	
	option java_package = "org.robocup_logistics.llsf_msgs";
	option java_outer_classname = "AttentionMessageProtos";
	
	message AttentionMessage {
	  enum CompType {
	    COMP_ID  = 2000;
	    MSG_TYPE = 2;
	  }
	
	  // The message to display, be brief!
	  required string message = 1;
	  // Time (sec) the msg should be visible
	  optional float  time_to_show = 2;
	  // if the message only regards one team
	  optional Team   team_color = 3;
	}
# <a name="SM2">BeaconSignal</a>
	package llsf_msgs;
	
	import "Time.proto";
	import "Team.proto";
	import "Pose2D.proto";
	
	option java_package =
	  "org.robocup_logistics.llsf_msgs";
	option java_outer_classname =
	  "BeaconSignalProtos";
	
	message BeaconSignal {
	  enum CompType {
	    COMP_ID  = 2000;
	    MSG_TYPE = 1;
	  }
	
	  // Local time in UTC
	  required Time   time = 1;
	  // Sequence number
	  required uint64 seq = 2;
	
	  // The robot's jersey number
	  required uint32 number = 8;
	  // The robot's team name
	  required string team_name = 4;
	  // The robot's name
	  required string peer_name = 5;
	  // Team color, teams MUST sent this
	  optional Team   team_color = 6;
	
	  // Position and orientation of the
	  // robot on the LLSF playing field
	  optional Pose2D pose = 7;
	}
# <a name="SM3">ExplorationInfo</a>
	package llsf_msgs;
	
	import "MachineInfo.proto";
	import "Pose2D.proto";
	import "Team.proto";
	import "Zone.proto";
	
	option java_package = "org.robocup_logistics.llsf_msgs";
	option java_outer_classname = "ExplorationInfoProtos";
	
	message ExplorationSignal {
	  enum CompType {
	    COMP_ID  = 2000;
	    MSG_TYPE = 70;
	  }
	
	  // machine type of this assignment
	  required string    type   = 1;
	  // Light specification (MachineInfo.proto)
	  repeated LightSpec lights = 2;
	}
	
	message ExplorationZone {
	  enum CompType {
	    COMP_ID  = 2000;
	    MSG_TYPE = 71;
	  }
	
	  // Zone to explore
	  required Zone  zone = 2;
	  // Team the machine belongs to
	  required Team  team_color = 3;
	}
	
	message ExplorationInfo {
	  enum CompType {
	    COMP_ID  = 2000;
	    MSG_TYPE = 72;
	  }
	
	  // The signal assignments
	  repeated ExplorationSignal  signals = 1;
	  // The zones to explore
	  repeated ExplorationZone    zones = 2;
	}
# <a name="SM4">GameInfo</a>
	package llsf_msgs;
	
	import "Team.proto";
	
	option java_package = "org.robocup_logistics.llsf_msgs";
	option java_outer_classname = "GameInfoProtos";
	
	// Game information for controllers
	message GameInfo {
	  enum CompType {
	    COMP_ID  = 2000;
	    MSG_TYPE = 81;
	  }
	
	  // The new desired phase
	  repeated string known_teams = 1;
	}
	
	// Request setting of a new game phase
	message SetTeamName {
	  enum CompType {
	    COMP_ID  = 2000;
	    MSG_TYPE = 82;
	  }
	
	  // Name of the team to set
	  required string team_name  = 1;
	
	  // Color of team
	  required Team   team_color = 2;
	}
# <a name="SM5">GameState</a>
	package llsf_msgs;
	
	import "Time.proto";
	
	option java_package = "org.robocup_logistics.llsf_msgs";
	option java_outer_classname = "GameStateProtos";
	
	message GameState {
	  enum CompType {
	    COMP_ID  = 2000;
	    MSG_TYPE = 20;
	  }
	
	  enum State {
	    INIT = 0;
	    WAIT_START = 1;
	    RUNNING = 2;
	    PAUSED = 3;
	  }
	
	  enum Phase {
	    PRE_GAME    = 0;
	    SETUP       = 10;
	    EXPLORATION = 20;
	    PRODUCTION  = 30;
	    POST_GAME   = 40;
	
	    OPEN_CHALLENGE         = 1000;
	    NAVIGATION_CHALLENGE   = 1001;
	    WHACK_A_MOLE_CHALLENGE = 1002;
	  }
	
	  enum RefBoxMode {
	    STANDALONE  = 0;
	    MASTER      = 1;
	    SLAVE       = 2;
	  }
	
	
	  // Time in seconds since game start
	  required Time   game_time = 1;
	
	  // Current game state
	  required State  state = 3;
	  // Current game phase
	  required Phase  phase = 4;
	  // Awarded points, cyan
	  optional uint32 points_cyan = 5;
	  // Name of the currently playing team
	  optional string team_cyan = 6;
	
	  // Awarded points, magenta
	  optional uint32 points_magenta = 8;
	  // Name of the currently playing team
	  optional string team_magenta = 9;
	
	  optional RefBoxMode refbox_mode = 7 [default = STANDALONE];
	}
	
	// Request setting of a new game state
	message SetGameState {
	  enum CompType {
	    COMP_ID  = 2000;
	    MSG_TYPE = 21;
	  }
	  // The new desired state
	  required GameState.State state = 1;
	}
	
	// Request setting of a new game phase
	message SetGamePhase {
	  enum CompType {
	    COMP_ID  = 2000;
	    MSG_TYPE = 22;
	  }
	  // The new desired phase
	  required GameState.Phase phase = 1;
	}
# <a name="SM6">MachineCommands</a>
	package llsf_msgs;
	
	option java_package = "org.robocup_logistics.llsf_msgs";
	option java_outer_classname = "MachineCommandsProtos";
	
	enum MachineState {
	  IDLE      = 1;
	  AVAILABLE = 2;
	  PROCESSED = 3;
	  DELIVERED = 4;
	  RETRIEVED = 5;
	}
	
	// Load puck into machine area.
	message SetMachineState {
	  enum CompType {
	    COMP_ID  = 2000;
	    MSG_TYPE = 17;
	  }
	
	  // Machine to place puck at
	  required string machine_name = 1;
	  // State to set
	  required MachineState state = 2;
	}
	
	
	// Load puck into machine area.
	message MachineAddBase {
	  enum CompType {
	    COMP_ID  = 2000;
	    MSG_TYPE = 18;
	  }
	
	  // Machine to place puck at
	  required string machine_name = 1;
	}
# <a name="SM7">MachineInfo</a>
	package llsf_msgs;
	
	import "Pose2D.proto";
	import "ProductColor.proto";
	import "Team.proto";
	import "Zone.proto";
	import "MachineInstructions.proto";
	
	option java_package = "org.robocup_logistics.llsf_msgs";
	option java_outer_classname = "MachineInfoProtos";
	
	enum LightColor {
	  RED = 0;
	  YELLOW = 1;
	  GREEN = 2;
	}
	
	enum LightState {
	  OFF = 0;
	  ON = 1;
	  BLINK = 2;
	}
	
	message LightSpec {
	  enum CompType {
	    COMP_ID  = 2000;
	    MSG_TYPE = 10;
	  }
	
	  // Color and state of described light
	  required LightColor color = 1;
	  required LightState state = 2;
	}
	
	message Machine {
	  enum CompType {
	    COMP_ID  = 2000;
	    MSG_TYPE = 12;
	  }
	  // Machine name, type, and team
	  required string    name       =  1;
	  optional string    type       =  2;
	  optional string    state      =  3;
	  optional Team      team_color = 10;
	
	  optional bool      prepared   = 15;
	
	  // Current state of the lights
	  repeated LightSpec lights = 7;
	  // Optional pose if known to refbox
	  optional Pose2D    pose = 8;
	  // Which zone the machine is in
	  optional Zone      zone = 11;
	  // Only set during exploration phase
	  // Correctly reported?
	  optional bool      correctly_reported = 9;
	  // Number of bases loaded
	  optional uint32    loaded_with = 13 [default = 0];
	
	  repeated RingColor ring_colors = 14;
	
	
	  // Instruction information
	  // only available to clients, not peers
	  optional PrepareInstructionBS instruction_bs = 16;
	  optional PrepareInstructionDS instruction_ds = 17;
	  optional PrepareInstructionRS instruction_rs = 18;
	  optional PrepareInstructionCS instruction_cs = 19;
	
	}
	
	message MachineInfo {
	  enum CompType {
	    COMP_ID  = 2000;
	    MSG_TYPE = 13;
	  }
	
	  // List of machines states
	  repeated Machine machines   = 1;
	
	  // Team name if all machines belong
	  // only to a single team (broadcast)
	  optional Team    team_color = 2;
	}
# <a name="SM8">MachineInstructions</a>
	package llsf_msgs;
	
	import "ProductColor.proto";
	import "Team.proto";
	
	option java_package = "org.robocup_logistics.llsf_msgs";
	option java_outer_classname = "MachineInstructionProtos";
	
	enum MachineSide {
	  INPUT  = 1;
	  OUTPUT = 2;
	}
	
	enum CsOp {
	  RETRIEVE_CAP = 1;
	  MOUNT_CAP    = 2;
	}
	
	message PrepareInstructionBS {
	  required MachineSide side  = 1;
	  required BaseColor   color = 2;
	}
	
	message PrepareInstructionDS {
	  required uint32 gate = 1;
	}
	
	message PrepareInstructionRS {
	  required RingColor ring_color = 1;
	}
	
	message PrepareInstructionCS {
	  required CsOp operation = 1;
	}
	
	message PrepareMachine {
	  enum CompType {
	    COMP_ID  = 2000;
	    MSG_TYPE = 101;
	  }
	
	  required Team   team_color = 1;
	  // Machine name which to instruct
	  required string machine = 2;
	
	  optional PrepareInstructionBS instruction_bs = 4;
	  optional PrepareInstructionDS instruction_ds = 5;
	  optional PrepareInstructionRS instruction_rs = 6;
	  optional PrepareInstructionCS instruction_cs = 7;
	}
# <a name="SM9">MachineReport</a>
	package llsf_msgs;
	
	import "MachineInfo.proto";
	import "Team.proto";
	import "Zone.proto";
	
	option java_package = "org.robocup_logistics.llsf_msgs";
	option java_outer_classname = "MachineReportProtos";
	
	message MachineReportEntry {
	  enum CompType {
	    COMP_ID  = 2000;
	    MSG_TYPE = 60;
	  }
	
	  // Machine name and recognized type
	  // and zone the machine is in
	  required string name = 1;
	  required string type = 2;
	  required Zone   zone = 3;
	}
	
	// Robots send this to announce recognized
	// machines to the refbox.
	message MachineReport {
	  enum CompType {
	    COMP_ID  = 2000;
	    MSG_TYPE = 61;
	  }
	
	  // Team for which the report is sent
	  required Team team_color = 2;
	
	  // All machines already already recognized
	  // or a subset thereof
	  repeated MachineReportEntry machines = 1;
	}
	
	
	// The refbox periodically sends this to
	// acknowledge reported machines
	message MachineReportInfo {
	  enum CompType {
	    COMP_ID  = 2000;
	    MSG_TYPE = 62;
	  }
	
	  // Names of machines for which the refbox
	  // received a report from a robot (which
	  // may have been correct or wrong)
	  repeated string reported_machines = 1;
	
	  // Team for which the report is sent
	  required Team team_color = 2;
	}
# <a name="SM10">OrderInfo</a>
	package llsf_msgs;
	
	import "Team.proto";
	import "ProductColor.proto";
	
	option java_package = "org.robocup_logistics.llsf_msgs";
	option java_outer_classname = "OrderInfoProtos";
	
	message Order {
	  enum CompType {
	    COMP_ID  = 2000;
	    MSG_TYPE = 42;
	  }
	
	  // Ordered product type
	  enum Complexity {
	    C0 = 0;
	    C1 = 1;
	    C2 = 2;
	    C3 = 3;
	  }
	
	  // ID and requested product of this order
	  required uint32       id = 1;
	  required Complexity   complexity = 2;
	
	  required BaseColor    base_color = 3;
	  repeated RingColor    ring_colors = 4;
	  required CapColor     cap_color = 5;
	
	  // Quantity requested and delivered
	  required uint32 quantity_requested = 6;
	  required uint32 quantity_delivered_cyan = 7;
	  required uint32 quantity_delivered_magenta = 8;
	
	  // Start and end time of the delivery
	  // period in seconds of game time
	  required uint32 delivery_period_begin = 9;
	  required uint32 delivery_period_end   = 10;
	
	  // The gate to deliver to, defaults to any
	  // (non-defunct, i.e. non-red light) gate
	  required uint32 delivery_gate = 11;
	
	}
	
	message OrderInfo {
	  enum CompType {
	    COMP_ID  = 2000;
	    MSG_TYPE = 41;
	  }
	
	  // The current orders
	  repeated Order orders = 1;
	}
	
	
	message SetOrderDelivered {
	  enum CompType {
	    COMP_ID  = 2000;
	    MSG_TYPE = 43;
	  }
	
	  required Team team_color = 1;
	  required uint32 order_id = 2;
	}
# <a name="SM11">Pose2D</a>
	package llsf_msgs;
	
	import "Time.proto";
	
	option java_package = "org.robocup_logistics.llsf_msgs";
	option java_outer_classname = "Pose2DProtos";
	
	// Pose information on 2D map
	// Data is relative to the LLSF field frame
	message Pose2D {
	  // Time when this pose was measured
	  required Time   timestamp = 1;
	
	  // X/Y coordinates in meters
	  required float  x = 2;
	  required float  y = 3;
	  // Orientation in rad
	  required float  ori = 4;
	}
# <a name="SM12">ProductColor</a>
	package llsf_msgs;
	
	option java_package = "org.robocup_logistics.llsf_msgs";
	option java_outer_classname = "ProductColorProtos";
	
	enum RingColor {
	  RING_BLUE   = 1;
	  RING_GREEN  = 2;
	  RING_ORANGE = 3;
	  RING_YELLOW = 4;
	}
	
	enum BaseColor {
	  BASE_RED = 1;
	  BASE_BLACK = 2;
	  BASE_SILVER = 3;
	}
	
	enum CapColor {
	  CAP_BLACK = 1;
	  CAP_GREY  = 2;
	}
# <a name="SM13">RingInfo</a>
	package llsf_msgs;
	
	import "ProductColor.proto";
	
	option java_package = "org.robocup_logistics.llsf_msgs";
	option java_outer_classname = "RingInfoProtos";
	
	
	message Ring {
	  // Ring color this concerns
	  required RingColor ring_color = 1;
	  // number of additional bases
	  // required to produce this ring type
	  required uint32    raw_material = 2;
	}
	
	message RingInfo {
	  enum CompType {
	    COMP_ID  = 2000;
	    MSG_TYPE = 110;
	  }
	
	  // List of all known pucks
	  repeated Ring rings = 1;
	}
# <a name="SM14">RobotCommands</a>
	package llsf_msgs;
	
	import "Team.proto";
	
	option java_package = "org.robocup_logistics.llsf_msgs";
	option java_outer_classname = "RobotCommandsProtos";
	
	// Set a robot's maintenance state
	message SetRobotMaintenance {
	  enum CompType {
	    COMP_ID  = 2000;
	    MSG_TYPE = 91;
	  }
	
	  // Number of robot to set state
	  required uint32 robot_number = 1;
	  // True to activate maintenance,
	  // false to bring back robot
	  required bool   maintenance  = 3;
	  // Team the robot belongs to
	  required Team   team_color   = 4;
	}
# <a name="SM15">RobotInfo</a>
	package llsf_msgs;
	
	import "Time.proto";
	import "Pose2D.proto";
	import "Team.proto";
	
	option java_package = "org.robocup_logistics.llsf_msgs";
	option java_outer_classname = "RobotInfoProtos";
	
	enum RobotState {
	  ACTIVE       = 1;
	  MAINTENANCE  = 2;
	  DISQUALIFIED = 3;
	}
	
	message Robot {
	  enum CompType {
	    COMP_ID  = 2000;
	    MSG_TYPE = 31;
	  }
	
	  // Name, team, and number of the robot
	  // as it was announced by the robot in
	  // the BeaconSignal message.
	  required string name = 1;
	  required string team = 2;
	  required Team   team_color = 12;
	  required uint32 number = 7;
	  // Host from where the BeaconSignal
	  // was received
	  required string host = 3;
	  // Timestamp in UTC when a BeaconSignal
	  // was received last from this robot
	  required Time   last_seen = 4;
	
	  // Pose information (reported by robot)
	  optional Pose2D pose = 6;
	  // Pose information (reported by vision)
	  optional Pose2D vision_pose = 11;
	
	  // Current state of this robot
	  optional RobotState state = 8;
	
	  // Time in seconds remaining in current
	  // maintenance cycle, negative if overdue
	  optional float  maintenance_time_remaining = 9 [default = 0.0];
	  // number of times maintenance
	  // has been performed, including current
	  optional uint32 maintenance_cycles = 10;
	}
	
	message RobotInfo {
	  enum CompType {
	    COMP_ID  = 2000;
	    MSG_TYPE = 30;
	  }
	
	  // List of all known robots
	  repeated Robot robots = 1;
	}
# <a name="SM16">SimTimeSync</a>
	package llsf_msgs;
	
	import "Time.proto";
	
	message SimTimeSync {
	  enum CompType {
	    COMP_ID  = 2000;
	    MSG_TYPE = 327;
	  }
	
	  required Time sim_time = 1;
	  required float real_time_factor = 2;
	  required bool paused = 3;
	}
# <a name="SM17">Team</a>
	package llsf_msgs;
	
	option java_package = "org.robocup_logistics.llsf_msgs";
	option java_outer_classname = "TeamProtos";
	
	// Team identifier.
	enum Team {
	  CYAN = 0;
	  MAGENTA = 1;
	}
# <a name="SM18">Time</a>
	package llsf_msgs;
	
	option java_package = "org.robocup_logistics.llsf_msgs";
	option java_outer_classname = "TimeProtos";
	
	// Time stamp and duration structure.
	// Can be used for absolute times or
	// durations alike.
	message Time {
	
	  // Time in seconds since the Unix epoch
	  // in UTC or seconds part of duration
	  required int64  sec = 1;
	
	  // Nano seconds after seconds for a time
	  // or nanoseconds part for duration
	  required int64 nsec = 2;
	}
# <a name="SM19">VersionInfo</a>
	package llsf_msgs;
	
	option java_package = "org.robocup_logistics.llsf_msgs";
	option java_outer_classname = "VersionProtos";
	
	message VersionInfo {
	  enum CompType {
	    COMP_ID  = 2000;
	    MSG_TYPE = 3;
	  }
	
	  required uint32 version_major  = 1;
	  required uint32 version_minor  = 2;
	  required uint32 version_micro  = 3;
	  required string version_string = 4;
	}
# <a name="SM20">Zone</a>
	package llsf_msgs;
	
	option java_package = "org.robocup_logistics.llsf_msgs";
	option java_outer_classname = "ZoneProtos";
	
	// Zone identifiers
	enum Zone {
	  Z1  =  1;
	  Z2  =  2;
	  Z3  =  3;
	  Z4  =  4;
	  Z5  =  5;
	  Z6  =  6;
	  Z7  =  7;
	  Z8  =  8;
	  Z9  =  9;
	  Z10 = 10;
	  Z11 = 11;
	  Z12 = 12;
	  Z13 = 13;
	  Z14 = 14;
	  Z15 = 15;
	  Z16 = 16;
	  Z17 = 17;
	  Z18 = 18;
	  Z19 = 19;
	  Z20 = 20;
	  Z21 = 21;
	  Z22 = 22;
	  Z23 = 23;
	  Z24 = 24;
	}
----
Last edited by Florian Gehrig at 30. Juni 2015