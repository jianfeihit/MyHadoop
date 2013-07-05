<script type="text/javascript" language="javascript" src="media/js/jquery.js"></script>
<script type="text/javascript" language="javascript" src="media/js/jquery.dataTables.min.js"></script>

<style type="text/css">
table th, table td {
word-wrap:break-word;
word-break:break-all;
}
#hadooptable {
	width:850px;
}
</style>

Hadoop参数汇总 
=======================
linux参数
-----------------------

1. 文件描述符 ulimit -n 
2. 用户最大进程 nproc （hbase需要[ hbse book]( http://hbase.apache.org/book.html#basic.prerequisites "hbase book")）
3. 关闭swap分区
4. 设置合理的预读取缓冲区
5. Linux的内核的IO调度器
table
JVM参数
-----------------------
[Hadoop Performance Tuning Guide](http://developer.amd.com/wordpress/media/2012/10/Hadoop_Tuning_Guide-Version5.pdf "Hadoop Performance Tuning Guide")

Hadoop参数大全
-----------------------
生成来源：4.3的default.xml，YarnConfiguration,MRJobConfig,JHAdminConfig

功能分类：
>
**重要**：NNHA,本地目录,HDFS目录，ip端口,垃圾回收，HDFS调优参数,
压缩,job,datanode,namenode,reduce，rmam,rm,nm,jobhistory
>
**重要但不常用**:ZKFC,安全,DNS,backupNode,balance,
staleDataNode,线程,speculative特性，uber特性，skip特性,end-notification特性,JobClient
>
**不重要**：日志，文件系统，FTP,httpfs，TFile,S3，KFS,顺序文件，映射文件，其它,secondary,jobtracker,tasktracker


重要度等级：
I9必须配置
i5配置了更好
I1基本不用管

<table cellpadding="0" cellspacing="0" border="0" class="display" id="hadooptable" width="100%">
<thead>
<tr>
<th width='40px'>版本</th>
<th width='40px'>文件位置</th>
<th width='40px'>分类</th>
<th width='100px'>名称</th>
<th width='200px'>描述</th>
<th width='80px'>默认值</th>
<th width='40px'>final</th>
<th width='40px'>推荐值</th>
<th width='40px'>重要度</th>
</thead>
<tbody>
<!-- replaceMark -->
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>hadoop.common.configuration.version</td>
<td>version of this configuration file</td>
<td>0.23.0</td>
<td> </td>
<td>0.23.0</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>本地目录</td>
<td>hadoop.tmp.dir</td>
<td>A base for other temporary directories.</td>
<td>/tmp/hadoop-${user.name}</td>
<td> </td>
<td>/tmp/hadoop-${user.name}</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>io.native.lib.available</td>
<td>Should native hadoop libraries, if present, be used.不适用本地库可以设置为false</td>
<td>true</td>
<td> </td>
<td>true</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.http.filter.initializers</td>
<td>A comma separated list of class names. Each class in the list 
  must extend org.apache.hadoop.http.FilterInitializer. The corresponding 
  Filter will be initialized. Then, the Filter will be applied to all user 
  facing jsp and servlet web pages.  The ordering of the list defines the 
  ordering of the filters.</td>
<td>org.apache.hadoop.http.lib.StaticUserWebFilter</td>
<td> </td>
<td>org.apache.hadoop.http.lib.StaticUserWebFilter</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.security.authorization</td>
<td>Is service-level authorization enabled?</td>
<td>false</td>
<td> </td>
<td>false</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.security.instrumentation.requires.admin</td>
<td>
    Indicates if administrator ACLs are required to access
    instrumentation servlets (JMX, METRICS, CONF, STACKS).
  </td>
<td>false</td>
<td> </td>
<td>false</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.security.authentication</td>
<td>Possible values are simple (no authentication), and kerberos
  </td>
<td>simple</td>
<td> </td>
<td>simple</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.security.group.mapping</td>
<td>
    Class for user to group mapping (get groups for a given user) for ACL. 
    The default implementation,
    org.apache.hadoop.security.JniBasedUnixGroupsMappingWithFallback, 
    will determine if the Java Native Interface (JNI) is available. If JNI is 
    available the implementation will use the API within hadoop to resolve a 
    list of groups for a user. If JNI is not available then the shell 
    implementation, ShellBasedUnixGroupsMapping, is used.  This implementation 
    shells out to the Linux/Unix environment with the 
    </td>
<td>org.apache.hadoop.security.JniBasedUnixGroupsMappingWithFallback</td>
<td> </td>
<td>org.apache.hadoop.security.JniBasedUnixGroupsMappingWithFallback</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.security.groups.cache.secs</td>
<td>
    This is the config controlling the validity of the entries in the cache
    containing the user->group mapping. When this duration has expired,
    then the implementation of the group mapping provider is invoked to get
    the groups of the user and then cached back.
  </td>
<td>300</td>
<td> </td>
<td>300</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.security.group.mapping.ldap.url</td>
<td>
    The URL of the LDAP server to use for resolving user groups when using
    the LdapGroupsMapping user to group mapping.
  </td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.security.group.mapping.ldap.ssl</td>
<td>
    Whether or not to use SSL when connecting to the LDAP server.
  </td>
<td>false</td>
<td> </td>
<td>false</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.security.group.mapping.ldap.ssl.keystore</td>
<td>
    File path to the SSL keystore that contains the SSL certificate required
    by the LDAP server.
  </td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.security.group.mapping.ldap.ssl.keystore.password.file</td>
<td>
    The path to a file containing the password of the LDAP SSL keystore.

    IMPORTANT: This file should be readable only by the Unix user running
    the daemons.
  </td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.security.group.mapping.ldap.bind.user</td>
<td>
    The distinguished name of the user to bind as when connecting to the LDAP
    server. This may be left blank if the LDAP server supports anonymous binds.
  </td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.security.group.mapping.ldap.bind.password.file</td>
<td>
    The path to a file containing the password of the bind user.

    IMPORTANT: This file should be readable only by the Unix user running
    the daemons.
  </td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.security.group.mapping.ldap.base</td>
<td>
    The search base for the LDAP connection. This is a distinguished name,
    and will typically be the root of the LDAP directory.
  </td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.security.group.mapping.ldap.search.filter.user</td>
<td>
    An additional filter to use when searching for LDAP users. The default will
    usually be appropriate for Active Directory installations. If connecting to
    an LDAP server with a non-AD schema, this should be replaced with
    (&(objectClass=inetOrgPerson)(uid={0}). {0} is a special string used to
    denote where the username fits into the filter.
  </td>
<td>(&(objectClass=user)(sAMAccountName={0}))</td>
<td> </td>
<td>(&(objectClass=user)(sAMAccountName={0}))</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.security.group.mapping.ldap.search.filter.group</td>
<td>
    An additional filter to use when searching for LDAP groups. This should be
    changed when resolving groups against a non-Active Directory installation.
    posixGroups are currently not a supported group class.
  </td>
<td>(objectClass=group)</td>
<td> </td>
<td>(objectClass=group)</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.security.group.mapping.ldap.search.attr.member</td>
<td>
    The attribute of the group object that identifies the users that are
    members of the group. The default will usually be appropriate for
    any LDAP installation.
  </td>
<td>member</td>
<td> </td>
<td>member</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.security.group.mapping.ldap.search.attr.group.name</td>
<td>
    The attribute of the group object that identifies the group name. The
    default will usually be appropriate for all LDAP systems.
  </td>
<td>cn</td>
<td> </td>
<td>cn</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.security.group.mapping.ldap.directory.search.timeout</td>
<td>
    The attribute applied to the LDAP SearchControl properties to set a
    maximum time limit when searching and awaiting a result.
    Set to 0 if infinite wait period is desired.
    Default is 10 seconds. Units in milliseconds.
  </td>
<td>10000</td>
<td> </td>
<td>10000</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.security.service.user.name.key</td>
<td>
    For those cases where the same RPC protocol is implemented by multiple
    servers, this configuration is required for specifying the principal
    name to use for the service when the client wishes to make an RPC call.
  </td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.security.uid.cache.secs</td>
<td>
        This is the config controlling the validity of the entries in the cache
        containing the userId to userName and groupId to groupName used by
        NativeIO getFstat().
    </td>
<td>14400</td>
<td> </td>
<td>14400</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.rpc.protection</td>
<td>This field sets the quality of protection for secured sasl 
      connections. Possible values are authentication, integrity and privacy.
      authentication means authentication only and no integrity or privacy; 
      integrity implies authentication and integrity are enabled; and privacy 
      implies all of authentication, integrity and privacy are enabled.
  </td>
<td>authentication</td>
<td> </td>
<td>authentication</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.work.around.non.threadsafe.getpwuid</td>
<td>Some operating systems or authentication modules are known to
  have broken implementations of getpwuid_r and getpwgid_r, such that these
  calls are not thread-safe. Symptoms of this problem include JVM crashes
  with a stack trace inside these functions. If your system exhibits this
  issue, enable this configuration parameter to include a lock around the
  calls as a workaround.

  An incomplete list of some systems known to have this issue is available
  at http://wiki.apache.org/hadoop/KnownBrokenPwuidImplementations
  </td>
<td>false</td>
<td> </td>
<td>false</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.kerberos.kinit.command</td>
<td>Used to periodically renew Kerberos credentials when provided
  to Hadoop. The default setting assumes that kinit is in the PATH of users
  running the Hadoop client. Change this to the absolute path to kinit if this
  is not the case.
  </td>
<td>kinit</td>
<td> </td>
<td>kinit</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.security.auth_to_local</td>
<td>Maps kerberos principals to local user names</td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>HDFS调优参数</td>
<td>io.file.buffer.size</td>
<td>The size of buffer for use in sequence files.
  The size of this buffer should probably be a multiple of hardware
  page size (4096 on Intel x86), and it determines how much data is
  buffered during read and write operations.</td>
<td>4096</td>
<td> </td>
<td>4096</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>io.bytes.per.checksum</td>
<td>The number of bytes per checksum.  Must not be larger than
  io.file.buffer.size.</td>
<td>512</td>
<td> </td>
<td>512</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>io.skip.checksum.errors</td>
<td>If true, when a checksum error is encountered while
  reading a sequence file, entries are skipped, instead of throwing an
  exception.</td>
<td>false</td>
<td> </td>
<td>false</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>压缩</td>
<td>io.compression.codecs</td>
<td>A comma-separated list of the compression codec classes that can
  be used for compression/decompression. In addition to any classes specified
  with this property (which take precedence), codec classes on the classpath
  are discovered using a Java ServiceLoader.</td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>io.serializations</td>
<td>A list of serialization classes that can be used for
  obtaining serializers and deserializers.</td>
<td>org.apache.hadoop.io.serializer.WritableSerialization,org.apache.hadoop.io.serializer.avro.AvroSpecificSerialization,org.apache.hadoop.io.serializer.avro.AvroReflectSerialization</td>
<td> </td>
<td>org.apache.hadoop.io.serializer.WritableSerialization,org.apache.hadoop.io.serializer.avro.AvroSpecificSerialization,org.apache.hadoop.io.serializer.avro.AvroReflectSerialization</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>本地目录</td>
<td>io.seqfile.local.dir</td>
<td>The local directory where sequence file stores intermediate
  data files during merge.  May be a comma-separated list of
  directories on different devices in order to spread disk i/o.
  Directories that do not exist are ignored.
  </td>
<td>${hadoop.tmp.dir}/io/local</td>
<td> </td>
<td>${hadoop.tmp.dir}/io/local</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>io.map.index.skip</td>
<td>Number of index entries to skip between each entry.
  Zero by default. Setting this to values larger than zero can
  facilitate opening large MapFiles using less memory.</td>
<td>0</td>
<td> </td>
<td>0</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>io.map.index.interval</td>
<td>
    MapFile consist of two files - data file (tuples) and index file
    (keys). For every io.map.index.interval records written in the
    data file, an entry (record-key, data-file-position) is written
    in the index file. This is to allow for doing binary search later
    within the index file to look up records by their keys and get their
    closest positions in the data file.
  </td>
<td>128</td>
<td> </td>
<td>128</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>HDFS目录</td>
<td>fs.defaultFS</td>
<td>The name of the default file system.  A URI whose
  scheme and authority determine the FileSystem implementation.  The
  uri's scheme determines the config property (fs.SCHEME.impl) naming
  the FileSystem implementation class.  The uri's authority is used to
  determine the host, port, etc. for a filesystem.</td>
<td>file:///</td>
<td> </td>
<td>hdfs://ip:port/</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>HDFS目录</td>
<td>fs.default.name</td>
<td>Deprecated. Use (fs.defaultFS) property
  instead</td>
<td>file:///</td>
<td> </td>
<td>hdfs://ip:port/</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>垃圾回收</td>
<td>fs.trash.interval</td>
<td>Number of minutes after which the checkpoint
  gets deleted.  If zero, the trash feature is disabled.
  This option may be configured both on the server and the
  client. If trash is disabled server side then the client
  side configuration is checked. If trash is enabled on the
  server side then the value configured on the server is
  used and the client configuration value is ignored.
  垃圾文件清空时间(分钟)
  </td>
<td>0</td>
<td> </td>
<td>4320</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>垃圾回收</td>
<td>fs.trash.checkpoint.interval</td>
<td>Number of minutes between trash checkpoints.
  Should be smaller or equal to fs.trash.interval. If zero,
  the value is set to the value of fs.trash.interval.
  Every time the checkpointer runs it creates a new checkpoint 
  out of current and removes checkpoints created more than 
  fs.trash.interval minutes ago.
  垃圾回收的间隔(分钟)
  </td>
<td>0</td>
<td> </td>
<td>0</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>文件系统</td>
<td>fs.AbstractFileSystem.file.impl</td>
<td>The AbstractFileSystem for file: uris.</td>
<td>org.apache.hadoop.fs.local.LocalFs</td>
<td> </td>
<td>org.apache.hadoop.fs.local.LocalFs</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>文件系统</td>
<td>fs.AbstractFileSystem.hdfs.impl</td>
<td>The FileSystem for hdfs: uris.</td>
<td>org.apache.hadoop.fs.Hdfs</td>
<td> </td>
<td>org.apache.hadoop.fs.Hdfs</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>文件系统</td>
<td>fs.AbstractFileSystem.viewfs.impl</td>
<td>The AbstractFileSystem for view file system for viewfs: uris
  (ie client side mount table:).</td>
<td>org.apache.hadoop.fs.viewfs.ViewFs</td>
<td> </td>
<td>org.apache.hadoop.fs.viewfs.ViewFs</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>FTP</td>
<td>fs.ftp.host</td>
<td>FTP filesystem connects to this server</td>
<td>0.0.0.0</td>
<td> </td>
<td>0.0.0.0</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>FTP</td>
<td>fs.ftp.host.port</td>
<td>
    FTP filesystem connects to fs.ftp.host on this port
  </td>
<td>21</td>
<td> </td>
<td>21</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>fs.df.interval</td>
<td>Disk usage statistics refresh interval in msec.</td>
<td>60000</td>
<td> </td>
<td>60000</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>S3文件系统</td>
<td>fs.s3.block.size</td>
<td>Block size to use when writing files to S3.</td>
<td>67108864</td>
<td> </td>
<td>67108864</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>S3文件系统</td>
<td>fs.s3.buffer.dir</td>
<td>Determines where on the local filesystem the S3 filesystem
  should store files before sending them to S3
  (or after retrieving them from S3).
  </td>
<td>${hadoop.tmp.dir}/s3</td>
<td> </td>
<td>${hadoop.tmp.dir}/s3</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>S3文件系统</td>
<td>fs.s3.maxRetries</td>
<td>The maximum number of retries for reading or writing files to S3, 
  before we signal failure to the application.
  </td>
<td>4</td>
<td> </td>
<td>4</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>S3文件系统</td>
<td>fs.s3.sleepTimeSeconds</td>
<td>The number of seconds to sleep between each S3 retry.
  </td>
<td>10</td>
<td> </td>
<td>10</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>文件系统</td>
<td>fs.automatic.close</td>
<td>By default, FileSystem instances are automatically closed at program
  exit using a JVM shutdown hook. Setting this property to false disables this
  behavior. This is an advanced option that should only be used by server applications
  requiring a more carefully orchestrated shutdown sequence.
  </td>
<td>true</td>
<td> </td>
<td>true</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>S3文件系统</td>
<td>fs.s3n.block.size</td>
<td>Block size to use when reading files using the native S3
  filesystem (s3n: URIs).</td>
<td>67108864</td>
<td> </td>
<td>67108864</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>顺序文件</td>
<td>io.seqfile.compress.blocksize</td>
<td>The minimum block size for compression in block compressed 
          SequenceFiles.
  </td>
<td>1000000</td>
<td> </td>
<td>1000000</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>顺序文件</td>
<td>io.seqfile.lazydecompress</td>
<td>Should values of block-compressed SequenceFiles be decompressed
          only when necessary.
  </td>
<td>true</td>
<td> </td>
<td>true</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>顺序文件</td>
<td>io.seqfile.sorter.recordlimit</td>
<td>The limit on number of records to be kept in memory in a spill 
          in SequenceFiles.Sorter
  </td>
<td>1000000</td>
<td> </td>
<td>1000000</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>映射文件</td>
<td>io.mapfile.bloom.size</td>
<td>The size of BloomFilter-s used in BloomMapFile. Each time this many
  keys is appended the next BloomFilter will be created (inside a DynamicBloomFilter).
  Larger values minimize the number of filters, which slightly increases the performance,
  but may waste too much space if the total number of keys is usually much smaller
  than this number.
  </td>
<td>1048576</td>
<td> </td>
<td>1048576</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>映射文件</td>
<td>io.mapfile.bloom.error.rate</td>
<td>The rate of false positives in BloomFilter-s used in BloomMapFile.
  As this value decreases, the size of BloomFilter-s increases exponentially. This
  value is the probability of encountering false positives (default is 0.5%).
  </td>
<td>0.005</td>
<td> </td>
<td>0.005</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>其它</td>
<td>hadoop.util.hash.type</td>
<td>The default implementation of Hash. Currently this can take one of the
  two values: 'murmur' to select MurmurHash and 'jenkins' to select JenkinsHash.
  </td>
<td>murmur</td>
<td> </td>
<td>murmur</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>客户端</td>
<td>ipc.client.idlethreshold</td>
<td>Defines the threshold number of connections after which
               connections will be inspected for idleness.
  </td>
<td>4000</td>
<td> </td>
<td>4000</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>ipc客户端</td>
<td>ipc.client.kill.max</td>
<td>Defines the maximum number of clients to disconnect in one go.
  </td>
<td>10</td>
<td> </td>
<td>10</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>ipc客户端</td>
<td>ipc.client.connection.maxidletime</td>
<td>The maximum time in msec after which a client will bring down the
               connection to the server.
  </td>
<td>10000</td>
<td> </td>
<td>10000</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>ipc客户端</td>
<td>ipc.client.connect.max.retries</td>
<td>Indicates the number of retries a client will make to establish
               a server connection.
  </td>
<td>10</td>
<td> </td>
<td>10</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>ipc客户端</td>
<td>ipc.client.connect.max.retries.on.timeouts</td>
<td>Indicates the number of retries a client will make on socket timeout
               to establish a server connection.
  </td>
<td>45</td>
<td> </td>
<td>45</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>ipc.server.listen.queue.size</td>
<td>Indicates the length of the listen queue for servers accepting
               client connections.
  </td>
<td>128</td>
<td> </td>
<td>128</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>ipc.server.tcpnodelay</td>
<td>Turn on/off Nagle's algorithm for the TCP socket connection on 
  the server. Setting to true disables the algorithm and may decrease latency
  with a cost of more/smaller packets. 
  </td>
<td>false</td>
<td> </td>
<td>false</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>ipc.client.tcpnodelay</td>
<td>Turn on/off Nagle's algorithm for the TCP socket connection on 
  the client. Setting to true disables the algorithm and may decrease latency
  with a cost of more/smaller packets. 
  </td>
<td>false</td>
<td> </td>
<td>false</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>hadoop.rpc.socket.factory.class.default</td>
<td> Default SocketFactory to use. This parameter is expected to be
    formatted as "package.FactoryClassName".
  </td>
<td>org.apache.hadoop.net.StandardSocketFactory</td>
<td> </td>
<td>org.apache.hadoop.net.StandardSocketFactory</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>hadoop.rpc.socket.factory.class.ClientProtocol</td>
<td> SocketFactory to use to connect to a DFS. If null or empty, use
    hadoop.rpc.socket.class.default. This socket factory is also used by
    DFSClient to create sockets to DataNodes.
  </td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>hadoop.socks.server</td>
<td> Address (host:port) of the SOCKS server to be used by the
    SocksSocketFactory.
  </td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>net.topology.node.switch.mapping.impl</td>
<td> The default implementation of the DNSToSwitchMapping. It
    invokes a script specified in net.topology.script.file.name to resolve
    node names. If the value for net.topology.script.file.name is not set, the
    default value of DEFAULT_RACK is returned for all node names.
  </td>
<td>org.apache.hadoop.net.ScriptBasedMapping</td>
<td> </td>
<td>org.apache.hadoop.net.ScriptBasedMapping</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>net.topology.script.file.name</td>
<td> The script name that should be invoked to resolve DNS names to
    NetworkTopology names. Example: the script would take host.foo.bar as an
    argument, and return /rack1 as the output.
  </td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>net.topology.script.number.args</td>
<td> The max number of args that the script configured with 
    net.topology.script.file.name should be run with. Each arg is an
    IP address.
  </td>
<td>100</td>
<td> </td>
<td>100</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>net.topology.table.file.name</td>
<td> The file name for a topology file, which is used when the
    net.topology.script.file.name property is set to
    org.apache.hadoop.net.TableMapping. The file format is a two column text
    file, with columns separated by whitespace. The first column is a DNS or
    IP address and the second column specifies the rack where the address maps.
    If no entry corresponding to a host in the cluster is found, then 
    /default-rack is assumed.
  </td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>file.stream-buffer-size</td>
<td>The size of buffer to stream files.
  The size of this buffer should probably be a multiple of hardware
  page size (4096 on Intel x86), and it determines how much data is
  buffered during read and write operations.</td>
<td>4096</td>
<td> </td>
<td>4096</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>file.bytes-per-checksum</td>
<td>The number of bytes per checksum.  Must not be larger than
  file.stream-buffer-size</td>
<td>512</td>
<td> </td>
<td>512</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>file.client-write-packet-size</td>
<td>Packet size for clients to write</td>
<td>65536</td>
<td> </td>
<td>65536</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>file.blocksize</td>
<td>Block size</td>
<td>67108864</td>
<td> </td>
<td>67108864</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>HDFS调优参数</td>
<td>file.replication</td>
<td>Replication factor</td>
<td>1</td>
<td> </td>
<td>1</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>s3.stream-buffer-size</td>
<td>The size of buffer to stream files.
  The size of this buffer should probably be a multiple of hardware
  page size (4096 on Intel x86), and it determines how much data is
  buffered during read and write operations.</td>
<td>4096</td>
<td> </td>
<td>4096</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>s3.bytes-per-checksum</td>
<td>The number of bytes per checksum.  Must not be larger than
  s3.stream-buffer-size</td>
<td>512</td>
<td> </td>
<td>512</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>s3.client-write-packet-size</td>
<td>Packet size for clients to write</td>
<td>65536</td>
<td> </td>
<td>65536</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>s3.blocksize</td>
<td>Block size</td>
<td>67108864</td>
<td> </td>
<td>67108864</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>s3.replication</td>
<td>Replication factor</td>
<td>3</td>
<td> </td>
<td>3</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>s3native.stream-buffer-size</td>
<td>The size of buffer to stream files.
  The size of this buffer should probably be a multiple of hardware
  page size (4096 on Intel x86), and it determines how much data is
  buffered during read and write operations.</td>
<td>4096</td>
<td> </td>
<td>4096</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>s3native.bytes-per-checksum</td>
<td>The number of bytes per checksum.  Must not be larger than
  s3native.stream-buffer-size</td>
<td>512</td>
<td> </td>
<td>512</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>s3native.client-write-packet-size</td>
<td>Packet size for clients to write</td>
<td>65536</td>
<td> </td>
<td>65536</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>s3native.blocksize</td>
<td>Block size</td>
<td>67108864</td>
<td> </td>
<td>67108864</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>s3native.replication</td>
<td>Replication factor</td>
<td>3</td>
<td> </td>
<td>3</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>kfs.stream-buffer-size</td>
<td>The size of buffer to stream files.
  The size of this buffer should probably be a multiple of hardware
  page size (4096 on Intel x86), and it determines how much data is
  buffered during read and write operations.</td>
<td>4096</td>
<td> </td>
<td>4096</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>KFS文件系统</td>
<td>kfs.bytes-per-checksum</td>
<td>The number of bytes per checksum.  Must not be larger than
  kfs.stream-buffer-size</td>
<td>512</td>
<td> </td>
<td>512</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>kfs.client-write-packet-size</td>
<td>Packet size for clients to write</td>
<td>65536</td>
<td> </td>
<td>65536</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>kfs.blocksize</td>
<td>Block size</td>
<td>67108864</td>
<td> </td>
<td>67108864</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>kfs.replication</td>
<td>Replication factor</td>
<td>3</td>
<td> </td>
<td>3</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>ftp.stream-buffer-size</td>
<td>The size of buffer to stream files.
  The size of this buffer should probably be a multiple of hardware
  page size (4096 on Intel x86), and it determines how much data is
  buffered during read and write operations.</td>
<td>4096</td>
<td> </td>
<td>4096</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>ftp.bytes-per-checksum</td>
<td>The number of bytes per checksum.  Must not be larger than
  ftp.stream-buffer-size</td>
<td>512</td>
<td> </td>
<td>512</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>none</td>
<td>ftp.client-write-packet-size</td>
<td>Packet size for clients to write</td>
<td>65536</td>
<td> </td>
<td>65536</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>FTP</td>
<td>ftp.blocksize</td>
<td>Block size</td>
<td>67108864</td>
<td> </td>
<td>67108864</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>FTP</td>
<td>ftp.replication</td>
<td>Replication factor</td>
<td>3</td>
<td> </td>
<td>3</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>TFile</td>
<td>tfile.io.chunk.size</td>
<td>
    Value chunk size in bytes. Default  to
    1MB. Values of the length less than the chunk size is
    guaranteed to have known value length in read time (See also
    TFile.Reader.Scanner.Entry.isValueLengthKnown()).
  </td>
<td>1048576</td>
<td> </td>
<td>1048576</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>TFile</td>
<td>tfile.fs.output.buffer.size</td>
<td>
    Buffer size used for FSDataOutputStream in bytes.
  </td>
<td>262144</td>
<td> </td>
<td>262144</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>TFile</td>
<td>tfile.fs.input.buffer.size</td>
<td>
    Buffer size used for FSDataInputStream in bytes.
  </td>
<td>262144</td>
<td> </td>
<td>262144</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.http.authentication.type</td>
<td>
    Defines authentication used for Oozie HTTP endpoint.
    Supported values are: simple | kerberos | #AUTHENTICATION_HANDLER_CLASSNAME#
  </td>
<td>simple</td>
<td> </td>
<td>simple</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.http.authentication.token.validity</td>
<td>
    Indicates how long (in seconds) an authentication token is valid before it has
    to be renewed.
  </td>
<td>36000</td>
<td> </td>
<td>36000</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.http.authentication.signature.secret.file</td>
<td>
    The signature secret for signing the authentication tokens.
    The same secret should be used for JT/NN/DN/TT configurations.
  </td>
<td>${user.home}/hadoop-http-auth-signature-secret</td>
<td> </td>
<td>${user.home}/hadoop-http-auth-signature-secret</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.http.authentication.cookie.domain</td>
<td>
    The domain to use for the HTTP cookie that stores the authentication token.
    In order to authentiation to work correctly across all Hadoop nodes web-consoles
    the domain must be correctly set.
    IMPORTANT: when using IP addresses, browsers ignore cookies with domain settings.
    For this setting to work properly all nodes in the cluster must be configured
    to generate URLs with hostname.domain names on it.
  </td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.http.authentication.simple.anonymous.allowed</td>
<td>
    Indicates if anonymous requests are allowed when using 'simple' authentication.
  </td>
<td>true</td>
<td> </td>
<td>true</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.http.authentication.kerberos.principal</td>
<td>
    Indicates the Kerberos principal to be used for HTTP endpoint.
    The principal MUST start with 'HTTP/' as per Kerberos HTTP SPNEGO specification.
  </td>
<td>HTTP/_HOST@LOCALHOST</td>
<td> </td>
<td>HTTP/_HOST@LOCALHOST</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.http.authentication.kerberos.keytab</td>
<td>
    Location of the keytab file with the credentials for the principal.
    Referring to the same keytab file Oozie uses for its Kerberos credentials for Hadoop.
  </td>
<td>${user.home}/hadoop.keytab</td>
<td> </td>
<td>${user.home}/hadoop.keytab</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>NNHA</td>
<td>dfs.ha.fencing.methods</td>
<td>
    List of fencing methods to use for service fencing. May contain
    builtin methods (eg shell and sshfence) or user-defined method.
  </td>
<td>null</td>
<td> </td>
<td>sshfence(hadoop:9922)</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>NNHA</td>
<td>dfs.ha.fencing.ssh.connect-timeout</td>
<td>
    SSH connection timeout, in milliseconds, to use with the builtin
    sshfence fencer.
  </td>
<td>30000</td>
<td> </td>
<td>30000</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>NNHA</td>
<td>dfs.ha.fencing.ssh.private-key-files</td>
<td>
    The SSH private key files to use with the builtin sshfence fencer.
  </td>
<td>null</td>
<td> </td>
<td>/home/hadoop/.ssh/id_rsa</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>NNHA</td>
<td>ha.zookeeper.quorum</td>
<td>
    A list of ZooKeeper server addresses, separated by commas, that are
    to be used by the ZKFailoverController in automatic failover.
	HA的ZK配置
  </td>
<td>null</td>
<td> </td>
<td>ip:port,ip:port</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>NNHA</td>
<td>ha.zookeeper.session-timeout.ms</td>
<td>
    The session timeout to use when the ZKFC connects to ZooKeeper.
    Setting this value to a lower value implies that server crashes
    will be detected more quickly, but risks triggering failover too
    aggressively in the case of a transient error or network blip.
  </td>
<td>5000</td>
<td> </td>
<td>5000</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>NNHA</td>
<td>ha.zookeeper.parent-znode</td>
<td>
    The ZooKeeper znode under which the ZK failover controller stores
    its information. Note that the nameservice ID is automatically
    appended to this znode, so it is not normally necessary to
    configure this, even in a federated environment.
  </td>
<td>/hadoop-ha</td>
<td> </td>
<td>/hadoop-ha</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>NNHA</td>
<td>ha.zookeeper.acl</td>
<td>
    A comma-separated list of ZooKeeper ACLs to apply to the znodes
    used by automatic failover. These ACLs are specified in the same
    format as used by the ZooKeeper CLI.

    If the ACL itself contains secrets, you may instead specify a
    path to a file, prefixed with the '@' symbol, and the value of
    this configuration will be loaded from within.
  </td>
<td>world:anyone:rwcda</td>
<td> </td>
<td>world:anyone:rwcda</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>NNHA</td>
<td>ha.zookeeper.auth</td>
<td>
    A comma-separated list of ZooKeeper authentications to add when
    connecting to ZooKeeper. These are specified in the same format
    as used by the "addauth" command in the ZK CLI. It is
    important that the authentications specified here are sufficient
    to access znodes with the ACL specified in ha.zookeeper.acl.

    If the auths contain secrets, you may instead specify a
    path to a file, prefixed with the '@' symbol, and the value of
    this configuration will be loaded from within.
  </td>
<td>null</td>
<td> </td>
<td>null</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>HDFS调优参数</td>
<td>hadoop.http.staticuser.user</td>
<td>
    The user name to filter as, on static web filters
    while rendering content. An example use is the HDFS
    web UI (user to be used for browsing files).
	界面上操作的用户的权限
  </td>
<td>dr.who</td>
<td> </td>
<td>hadoop</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.ssl.keystores.factory.class</td>
<td>
    The keystores factory to use for retrieving certificates.
  </td>
<td>org.apache.hadoop.security.ssl.FileBasedKeyStoresFactory</td>
<td> </td>
<td>org.apache.hadoop.security.ssl.FileBasedKeyStoresFactory</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.ssl.require.client.cert</td>
<td>Whether client certificates are required</td>
<td>false</td>
<td> </td>
<td>false</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.ssl.hostname.verifier</td>
<td>
    The hostname verifier to provide for HttpsURLConnections.
    Valid values are: DEFAULT, STRICT, STRICT_I6, DEFAULT_AND_LOCALHOST and
    ALLOW_ALL
  </td>
<td>DEFAULT</td>
<td> </td>
<td>DEFAULT</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.ssl.server.conf</td>
<td>
    Resource file from which ssl server keystore information will be extracted.
    This file is looked up in the classpath, typically it should be in Hadoop
    conf/ directory.
  </td>
<td>ssl-server.xml</td>
<td> </td>
<td>ssl-server.xml</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.ssl.client.conf</td>
<td>
    Resource file from which ssl client keystore information will be extracted
    This file is looked up in the classpath, typically it should be in Hadoop
    conf/ directory.
  </td>
<td>ssl-client.xml</td>
<td> </td>
<td>ssl-client.xml</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>安全</td>
<td>hadoop.ssl.enabled</td>
<td>
    Whether to use SSL for the HTTP endpoints. If set to true, the
    NameNode, DataNode, ResourceManager, NodeManager, HistoryServer and
    MapReduceAppMaster web UIs will be served over HTTPS instead HTTP.
  </td>
<td>false</td>
<td> </td>
<td>false</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>其它</td>
<td>hadoop.jetty.logs.serve.aliases</td>
<td>
    Enable/Disable aliases serving from jetty
  </td>
<td>true</td>
<td> </td>
<td>true</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>HDFS调优参数</td>
<td>fs.permissions.umask-mode</td>
<td>
    The umask used when creating files and directories.
    Can be in octal or in symbolic. Examples are:
    "022" (octal for u=rwx,g=r-x,o=r-x in symbolic),
    or "u=rwx,g=rwx,o=" (symbolic for 007 in octal).
  </td>
<td>022</td>
<td> </td>
<td>022</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>ZKFC</td>
<td>ha.health-monitor.connect-retry-interval.ms</td>
<td>
    How often to retry connecting to the service.
  </td>
<td>1000</td>
<td> </td>
<td>1000</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>ZKFC</td>
<td>ha.health-monitor.check-interval.ms</td>
<td>
    How often to check the service.
  </td>
<td>1000</td>
<td> </td>
<td>1000</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>ZKFC</td>
<td>ha.health-monitor.sleep-after-disconnect.ms</td>
<td>
    How long to sleep after an unexpected RPC error.
  </td>
<td>1000</td>
<td> </td>
<td>1000</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>ZKFC</td>
<td>ha.health-monitor.rpc-timeout.ms</td>
<td>
    Timeout for the actual monitorHealth() calls.
  </td>
<td>45000</td>
<td> </td>
<td>45000</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>ZKFC</td>
<td>ha.failover-controller.new-active.rpc-timeout.ms</td>
<td>
    Timeout that the FC waits for the new active to become active
  </td>
<td>60000</td>
<td> </td>
<td>60000</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>ZKFC</td>
<td>ha.failover-controller.graceful-fence.rpc-timeout.ms</td>
<td>
    Timeout that the FC waits for the old active to go to standby
  </td>
<td>5000</td>
<td> </td>
<td>5000</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>ZKFC</td>
<td>ha.failover-controller.graceful-fence.connection.retries</td>
<td>
    FC connection retries for graceful fencing
  </td>
<td>1</td>
<td> </td>
<td>1</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>core-default.xml</td>
<td>ZKFC</td>
<td>ha.failover-controller.cli-check.rpc-timeout.ms</td>
<td>
    Timeout that the CLI (manual) FC waits for monitorHealth, getServiceState
  </td>
<td>20000</td>
<td> </td>
<td>20000</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>none</td>
<td>hadoop.hdfs.configuration.version</td>
<td>version of this configuration file</td>
<td>1</td>
<td> </td>
<td>1</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>日志</td>
<td>dfs.namenode.logging.level</td>
<td>
    The logging level for dfs namenode. Other values are "dir" (trace
    namespace mutations), "block" (trace block under/over replications
    and block creations/deletions), or "all".
  </td>
<td>info</td>
<td> </td>
<td>info</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>ip端口</td>
<td>dfs.namenode.secondary.http-address</td>
<td>
    The secondary namenode http server address and port.
    If the port is 0 then the server will start on a free port.
  </td>
<td>0.0.0.0:50090</td>
<td> </td>
<td>0.0.0.0:50090</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>ip端口</td>
<td>dfs.datanode.address</td>
<td>
    The datanode server address and port for data transfer.
    If the port is 0 then the server will start on a free port.
  </td>
<td>0.0.0.0:50010</td>
<td> </td>
<td>0.0.0.0:50010</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>ip端口</td>
<td>dfs.datanode.http.address</td>
<td>
    The datanode http server address and port.
    If the port is 0 then the server will start on a free port.
  </td>
<td>0.0.0.0:50075</td>
<td> </td>
<td>0.0.0.0:50075</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>ip端口</td>
<td>dfs.datanode.ipc.address</td>
<td>
    The datanode ipc server address and port.
    If the port is 0 then the server will start on a free port.
  </td>
<td>0.0.0.0:50020</td>
<td> </td>
<td>0.0.0.0:50020</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>datanode</td>
<td>dfs.datanode.handler.count</td>
<td>The number of server threads for the datanode.</td>
<td>10</td>
<td> </td>
<td>10</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>ip端口</td>
<td>dfs.namenode.http-address</td>
<td>
    The address and the base port where the dfs namenode web ui will listen on.
    If the port is 0 then the server will start on a free port.
  </td>
<td>0.0.0.0:50070</td>
<td> </td>
<td>0.0.0.0:50070</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>安全</td>
<td>dfs.https.enable</td>
<td>Decide if HTTPS(SSL) is supported on HDFS
  </td>
<td>false</td>
<td> </td>
<td>false</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>安全</td>
<td>dfs.client.https.need-auth</td>
<td>Whether SSL client certificate authentication is required
  </td>
<td>false</td>
<td> </td>
<td>false</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>安全</td>
<td>dfs.https.server.keystore.resource</td>
<td>Resource file from which ssl server keystore
  information will be extracted
  </td>
<td>ssl-server.xml</td>
<td> </td>
<td>ssl-server.xml</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>安全</td>
<td>dfs.client.https.keystore.resource</td>
<td>Resource file from which ssl client keystore
  information will be extracted
  </td>
<td>ssl-client.xml</td>
<td> </td>
<td>ssl-client.xml</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>ip端口</td>
<td>dfs.datanode.https.address</td>
<td>The datanode secure http server address and port.</td>
<td>0.0.0.0:50475</td>
<td> </td>
<td>0.0.0.0:50475</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>ip端口</td>
<td>dfs.namenode.https-address</td>
<td>The namenode secure http server address and port.</td>
<td>0.0.0.0:50470</td>
<td> </td>
<td>0.0.0.0:50470</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>DNS</td>
<td>dfs.datanode.dns.interface</td>
<td>The name of the Network Interface from which a data node should 
  report its IP address.
  </td>
<td>default</td>
<td> </td>
<td>default</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>DNS</td>
<td>dfs.datanode.dns.nameserver</td>
<td>The host name or IP address of the name server (DNS)
  which a DataNode should use to determine the host name used by the
  NameNode for communication and display purposes.
  </td>
<td>default</td>
<td> </td>
<td>default</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>backupNode</td>
<td>dfs.namenode.backup.address</td>
<td>
    The backup node server address and port.
    If the port is 0 then the server will start on a free port.
  </td>
<td>0.0.0.0:50100</td>
<td> </td>
<td>0.0.0.0:50100</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>backupNode</td>
<td>dfs.namenode.backup.http-address</td>
<td>
    The backup node http server address and port.
    If the port is 0 then the server will start on a free port.
  </td>
<td>0.0.0.0:50105</td>
<td> </td>
<td>0.0.0.0:50105</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>namenode</td>
<td>dfs.namenode.replication.considerLoad</td>
<td>Decide if chooseTarget considers the target's load or not
  </td>
<td>true</td>
<td> </td>
<td>true</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>none</td>
<td>dfs.default.chunk.view.size</td>
<td>The number of bytes to view for a file on the browser.
  </td>
<td>32768</td>
<td> </td>
<td>32768</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>datanode</td>
<td>dfs.datanode.du.reserved</td>
<td>Reserved space in bytes per volume. Always leave this much space free for non dfs use.
  </td>
<td>0</td>
<td> </td>
<td>0</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>本地目录</td>
<td>dfs.namenode.name.dir</td>
<td>Determines where on the local filesystem the DFS name node
      should store the name table(fsimage).  If this is a comma-delimited list
      of directories then the name table is replicated in all of the
      directories, for redundancy. </td>
<td>file://${hadoop.tmp.dir}/dfs/name</td>
<td> </td>
<td>file://${hadoop.tmp.dir}/dfs/name</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>namenode</td>
<td>dfs.namenode.name.dir.restore</td>
<td>Set to true to enable NameNode to attempt recovering a
      previously failed dfs.namenode.name.dir. When enabled, a recovery of any
      failed directory is attempted during checkpoint.</td>
<td>false</td>
<td> </td>
<td>false</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>namenode</td>
<td>dfs.namenode.fs-limits.max-component-length</td>
<td>Defines the maximum number of characters in each component
      of a path.  A value of 0 will disable the check.
	  文件长度限制</td>
<td>0</td>
<td> </td>
<td>0</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>namenode</td>
<td>dfs.namenode.fs-limits.max-directory-items</td>
<td>Defines the maximum number of items that a directory may
      contain.  A value of 0 will disable the check.
	  目录长度限制</td>
<td>0</td>
<td> </td>
<td>0</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>namenode</td>
<td>dfs.namenode.fs-limits.min-block-size</td>
<td>Minimum block size in bytes, enforced by the Namenode at create
      time. This prevents the accidental creation of files with tiny block
      sizes (and thus many blocks), which can degrade
      performance.
	  客户端可指定的最小的blocksize</td>
<td>1048576</td>
<td> </td>
<td>1048576</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>none</td>
<td>dfs.namenode.fs-limits.max-blocks-per-file</td>
<td>Maximum number of blocks per file, enforced by the Namenode on
        write. This prevents the creation of extremely large files which can
        degrade performance.
		文件的最大block数量</td>
<td>1048576</td>
<td> </td>
<td>1048576</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>本地目录</td>
<td>dfs.namenode.edits.dir</td>
<td>Determines where on the local filesystem the DFS name node
      should store the transaction (edits) file. If this is a comma-delimited list
      of directories then the transaction file is replicated in all of the 
      directories, for redundancy. Default value is same as dfs.namenode.name.dir
  </td>
<td>${dfs.namenode.name.dir}</td>
<td> </td>
<td>${dfs.namenode.name.dir}</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>QJM</td>
<td>dfs.namenode.shared.edits.dir</td>
<td>A directory on shared storage between the multiple namenodes
  in an HA cluster. This directory will be written by the active and read
  by the standby in order to keep the namespaces synchronized. This directory
  does not need to be listed in dfs.namenode.edits.dir above. It should be
  left empty in a non-HA cluster.
  </td>
<td>null</td>
<td> </td>
<td>qjournal://ip:host;ip:host;ip:host/mycluster</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>QJM</td>
<td>dfs.namenode.edits.journal-plugin.qjournal</td>
<td>null</td>
<td>org.apache.hadoop.hdfs.qjournal.client.QuorumJournalManager</td>
<td> </td>
<td>org.apache.hadoop.hdfs.qjournal.client.QuorumJournalManager</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>安全</td>
<td>dfs.permissions.enabled</td>
<td>
    If "true", enable permission checking in HDFS.
    If "false", permission checking is turned off,
    but all other behavior is unchanged.
    Switching from one parameter value to the other does not change the mode,
    owner or group of files or directories.
  </td>
<td>true</td>
<td> </td>
<td>true</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>安全</td>
<td>dfs.permissions.superusergroup</td>
<td>The name of the group of super-users.</td>
<td>supergroup</td>
<td> </td>
<td>supergroup</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>安全</td>
<td>dfs.block.access.token.enable</td>
<td>
    If "true", access tokens are used as capabilities for accessing datanodes.
    If "false", no access tokens are checked on accessing datanodes.
  </td>
<td>false</td>
<td> </td>
<td>false</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>安全</td>
<td>dfs.block.access.key.update.interval</td>
<td>
    Interval in minutes at which namenode updates its access keys.
  </td>
<td>600</td>
<td> </td>
<td>600</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>安全</td>
<td>dfs.block.access.token.lifetime</td>
<td>The lifetime of access tokens in minutes.</td>
<td>600</td>
<td> </td>
<td>600</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>本地目录</td>
<td>dfs.datanode.data.dir</td>
<td>Determines where on the local filesystem an DFS data node
  should store its blocks.  If this is a comma-delimited
  list of directories, then data will be stored in all named
  directories, typically on different devices.
  Directories that do not exist are ignored.
  必须创建文件夹，否则被视为不存在
  </td>
<td>file://${hadoop.tmp.dir}/dfs/data</td>
<td> </td>
<td>file://${hadoop.tmp.dir}/dfs/data</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>权限</td>
<td>dfs.datanode.data.dir.perm</td>
<td>Permissions for the directories on on the local filesystem where
  the DFS data node store its blocks. The permissions can either be octal or
  symbolic.</td>
<td>700</td>
<td> </td>
<td>700</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>hdfs参数调优</td>
<td>dfs.replication</td>
<td>Default block replication. 
  The actual number of replications can be specified when the file is created.
  The default is used if replication is not specified in create time.
  </td>
<td>3</td>
<td> </td>
<td>3</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>hdfs参数调优</td>
<td>dfs.replication.max</td>
<td>Maximal block replication. 
  </td>
<td>512</td>
<td> </td>
<td>512</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>hdfs参数调优</td>
<td>dfs.namenode.replication.min</td>
<td>Minimal block replication. 
  </td>
<td>1</td>
<td> </td>
<td>1</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>hdfs参数调优</td>
<td>dfs.blocksize</td>
<td>
      The default block size for new files, in bytes.
      You can use the following suffix (case insensitive):
      k(kilo), m(mega), g(giga), t(tera), p(peta), e(exa) to specify the size (such as 128k, 512m, 1g, etc.),
      Or provide complete size in bytes (such as 134217728 for 128 MB).
  </td>
<td>67108864</td>
<td> </td>
<td>67108864</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>hdfs客户端</td>
<td>dfs.client.block.write.retries</td>
<td>The number of retries for writing blocks to the data nodes, 
  before we signal failure to the application.
  </td>
<td>3</td>
<td> </td>
<td>3</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>hdfs客户端</td>
<td>dfs.client.block.write.replace-datanode-on-failure.enable</td>
<td>
    If there is a datanode/network failure in the write pipeline,
    DFSClient will try to remove the failed datanode from the pipeline
    and then continue writing with the remaining datanodes. As a result,
    the number of datanodes in the pipeline is decreased.  The feature is
    to add new datanodes to the pipeline.

    This is a site-wide property to enable/disable the feature.

    When the cluster size is extremely small, e.g. 3 nodes or less, cluster
    administrators may want to set the policy to NEVER in the default
    configuration file or disable this feature.  Otherwise, users may
    experience an unusually high rate of pipeline failures since it is
    impossible to find new datanodes for replacement.

    See also dfs.client.block.write.replace-datanode-on-failure.policy
  </td>
<td>true</td>
<td> </td>
<td>true</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>hdfs客户端</td>
<td>dfs.client.block.write.replace-datanode-on-failure.policy</td>
<td>
    This property is used only if the value of
    dfs.client.block.write.replace-datanode-on-failure.enable is true.

    ALWAYS: always add a new datanode when an existing datanode is removed.
    
    NEVER: never add a new datanode.

    DEFAULT: 
      Let r be the replication number.
      Let n be the number of existing datanodes.
      Add a new datanode only if r is greater than or equal to 3 and either
      (1) floor(r/2) is greater than or equal to n; or
      (2) r is greater than n and the block is hflushed/appended.
  </td>
<td>DEFAULT</td>
<td> </td>
<td>DEFAULT</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>datanode</td>
<td>dfs.blockreport.intervalMsec</td>
<td>Determines block reporting interval in milliseconds.</td>
<td>21600000</td>
<td> </td>
<td>21600000</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>datanode</td>
<td>dfs.blockreport.initialDelay</td>
<td>Delay for first block report in seconds.</td>
<td>0</td>
<td> </td>
<td>0</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>datanode</td>
<td>dfs.datanode.directoryscan.interval</td>
<td>Interval in seconds for Datanode to scan data directories and
  reconcile the difference between blocks in memory and on the disk.
  </td>
<td>21600</td>
<td> </td>
<td>21600</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>datanode</td>
<td>dfs.datanode.directoryscan.threads</td>
<td>How many threads should the threadpool used to compile reports
  for volumes in parallel have.
  </td>
<td>1</td>
<td> </td>
<td>1</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>datanode</td>
<td>dfs.heartbeat.interval</td>
<td>Determines datanode heartbeat interval in seconds.</td>
<td>3</td>
<td> </td>
<td>3</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>namenode</td>
<td>dfs.namenode.handler.count</td>
<td>The number of server threads for the namenode.</td>
<td>10</td>
<td> </td>
<td>10</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>namenode</td>
<td>dfs.namenode.safemode.threshold-pct</td>
<td>
    Specifies the percentage of blocks that should satisfy 
    the minimal replication requirement defined by dfs.namenode.replication.min.
    Values less than or equal to 0 mean not to wait for any particular
    percentage of blocks before exiting safemode.
    Values greater than 1 will make safe mode permanent.
  </td>
<td>0.999f</td>
<td> </td>
<td>0.999f</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>namenode</td>
<td>dfs.namenode.safemode.min.datanodes</td>
<td>
    Specifies the number of datanodes that must be considered alive
    before the name node exits safemode.
    Values less than or equal to 0 mean not to take the number of live
    datanodes into account when deciding whether to remain in safe mode
    during startup.
    Values greater than the number of datanodes in the cluster
    will make safe mode permanent.
  </td>
<td>0</td>
<td> </td>
<td>0</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>namenode</td>
<td>dfs.namenode.safemode.extension</td>
<td>
    Determines extension of safe mode in milliseconds 
    after the threshold level is reached.
  </td>
<td>30000</td>
<td> </td>
<td>30000</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>balance</td>
<td>dfs.datanode.balance.bandwidthPerSec</td>
<td>
        Specifies the maximum amount of bandwidth that each datanode
        can utilize for the balancing purpose in term of
        the number of bytes per second.
  </td>
<td>1048576</td>
<td> </td>
<td>1048576</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>namenode</td>
<td>dfs.hosts</td>
<td>Names a file that contains a list of hosts that are
  permitted to connect to the namenode. The full pathname of the file
  must be specified.  If the value is empty, all hosts are
  permitted.</td>
<td>null</td>
<td> </td>
<td>null</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>namenode</td>
<td>dfs.hosts.exclude</td>
<td>Names a file that contains a list of hosts that are
  not permitted to connect to the namenode.  The full pathname of the
  file must be specified.  If the value is empty, no hosts are
  excluded.</td>
<td>null</td>
<td> </td>
<td>null</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>namenode</td>
<td>dfs.namenode.max.objects</td>
<td>The maximum number of files, directories and blocks
  dfs supports. A value of zero indicates no limit to the number
  of objects that dfs supports.
  </td>
<td>0</td>
<td> </td>
<td>0</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>namenode</td>
<td>dfs.namenode.decommission.interval</td>
<td>Namenode periodicity in seconds to check if decommission is 
  complete.</td>
<td>30</td>
<td> </td>
<td>30</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>namenode</td>
<td>dfs.namenode.decommission.nodes.per.interval</td>
<td>The number of nodes namenode checks if decommission is complete
  in each dfs.namenode.decommission.interval.</td>
<td>5</td>
<td> </td>
<td>5</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>namenode</td>
<td>dfs.namenode.replication.interval</td>
<td>The periodicity in seconds with which the namenode computes 
  repliaction work for datanodes. </td>
<td>3</td>
<td> </td>
<td>3</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>namenode</td>
<td>dfs.namenode.accesstime.precision</td>
<td>The access time for HDFS file is precise upto this value. 
               The default value is 1 hour. Setting a value of 0 disables
               access times for HDFS.
  </td>
<td>3600000</td>
<td> </td>
<td>3600000</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>datanode</td>
<td>dfs.datanode.plugins</td>
<td>Comma-separated list of datanode plug-ins to be activated.
  </td>
<td>null</td>
<td> </td>
<td>null</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>namenode</td>
<td>dfs.namenode.plugins</td>
<td>Comma-separated list of namenode plug-ins to be activated.
  </td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>hdfs参数调优</td>
<td>dfs.stream-buffer-size</td>
<td>The size of buffer to stream files.
  The size of this buffer should probably be a multiple of hardware
  page size (4096 on Intel x86), and it determines how much data is
  buffered during read and write operations.</td>
<td>4096</td>
<td> </td>
<td>4096</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>hdfs参数调优</td>
<td>dfs.bytes-per-checksum</td>
<td>The number of bytes per checksum.  Must not be larger than
  dfs.stream-buffer-size</td>
<td>512</td>
<td> </td>
<td>512</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>hdfs参数调优</td>
<td>dfs.client-write-packet-size</td>
<td>Packet size for clients to write</td>
<td>65536</td>
<td> </td>
<td>65536</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>hdfs参数调优</td>
<td>dfs.client.write.exclude.nodes.cache.expiry.interval.millis</td>
<td>The maximum period to keep a DN in the excluded nodes list
  at a client. After this period, in milliseconds, the previously excluded node(s) will
  be removed automatically from the cache and will be considered good for block allocations
  again. Useful to lower or raise in situations where you keep a file open for very long
  periods (such as a Write-Ahead-Log (WAL) file) to make the writer tolerant to cluster maintenance
  restarts. Defaults to 10 minutes.</td>
<td>600000</td>
<td> </td>
<td>600000</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>secondary</td>
<td>dfs.namenode.checkpoint.dir</td>
<td>Determines where on the local filesystem the DFS secondary
      name node should store the temporary images to merge.
      If this is a comma-delimited list of directories then the image is
      replicated in all of the directories for redundancy.
  </td>
<td>file://${hadoop.tmp.dir}/dfs/namesecondary</td>
<td> </td>
<td>file://${hadoop.tmp.dir}/dfs/namesecondary</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>secondary</td>
<td>dfs.namenode.checkpoint.edits.dir</td>
<td>Determines where on the local filesystem the DFS secondary
      name node should store the temporary edits to merge.
      If this is a comma-delimited list of directoires then teh edits is
      replicated in all of the directoires for redundancy.
      Default value is same as dfs.namenode.checkpoint.dir
  </td>
<td>${dfs.namenode.checkpoint.dir}</td>
<td> </td>
<td>${dfs.namenode.checkpoint.dir}</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>secondary</td>
<td>dfs.namenode.checkpoint.period</td>
<td>The number of seconds between two periodic checkpoints.
  </td>
<td>3600</td>
<td> </td>
<td>3600</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>secondary</td>
<td>dfs.namenode.checkpoint.txns</td>
<td>The Secondary NameNode or CheckpointNode will create a checkpoint
  of the namespace every 'dfs.namenode.checkpoint.txns' transactions, regardless
  of whether 'dfs.namenode.checkpoint.period' has expired.
  </td>
<td>1000000</td>
<td> </td>
<td>1000000</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>secondary</td>
<td>dfs.namenode.checkpoint.check.period</td>
<td>The SecondaryNameNode and CheckpointNode will poll the NameNode
  every 'dfs.namenode.checkpoint.check.period' seconds to query the number
  of uncheckpointed transactions.
  </td>
<td>60</td>
<td> </td>
<td>60</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>secondary</td>
<td>dfs.namenode.checkpoint.max-retries</td>
<td>The SecondaryNameNode retries failed checkpointing. If the 
  failure occurs while loading fsimage or replaying edits, the number of
  retries is limited by this variable. 
  </td>
<td>3</td>
<td> </td>
<td>3</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>secondary</td>
<td>dfs.namenode.num.checkpoints.retained</td>
<td>The number of image checkpoint files that will be retained by
  the NameNode and Secondary NameNode in their storage directories. All edit
  logs necessary to recover an up-to-date namespace from the oldest retained
  checkpoint will also be retained.
  </td>
<td>2</td>
<td> </td>
<td>2</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>NNHA</td>
<td>dfs.namenode.num.extra.edits.retained</td>
<td>The number of extra transactions which should be retained
  beyond what is minimally necessary for a NN restart. This can be useful for
  audit purposes or for an HA setup where a remote Standby Node may have
  been offline for some time and need to have a longer backlog of retained
  edits in order to start again.
  Typically each edit is on the order of a few hundred bytes, so the default
  of 1 million edits should be on the order of hundreds of MBs or low GBs.

  NOTE: Fewer extra edits may be retained than value specified for this setting
  if doing so would mean that more segments would be retained than the number
  configured by dfs.namenode.max.extra.edits.segments.retained.
  </td>
<td>1000000</td>
<td> </td>
<td>1000000</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>NNHA</td>
<td>dfs.namenode.max.extra.edits.segments.retained</td>
<td>The maximum number of extra edit log segments which should be retained
  beyond what is minimally necessary for a NN restart. When used in conjunction with
  dfs.namenode.num.extra.edits.retained, this configuration property serves to cap
  the number of extra edits files to a reasonable value.
  </td>
<td>10000</td>
<td> </td>
<td>10000</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>安全</td>
<td>dfs.namenode.delegation.key.update-interval</td>
<td>The update interval for master key for delegation tokens 
       in the namenode in milliseconds.
  </td>
<td>86400000</td>
<td> </td>
<td>86400000</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>安全</td>
<td>dfs.namenode.delegation.token.max-lifetime</td>
<td>The maximum lifetime in milliseconds for which a delegation 
      token is valid.
  </td>
<td>604800000</td>
<td> </td>
<td>604800000</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>安全</td>
<td>dfs.namenode.delegation.token.renew-interval</td>
<td>The renewal interval for delegation token in milliseconds.
  </td>
<td>86400000</td>
<td> </td>
<td>86400000</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>datanode</td>
<td>dfs.datanode.failed.volumes.tolerated</td>
<td>The number of volumes that are allowed to
  fail before a datanode stops offering service. By default
  any volume failure will cause a datanode to shutdown.
  </td>
<td>0</td>
<td> </td>
<td>0</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>namenode</td>
<td>dfs.image.compress</td>
<td>Should the dfs image be compressed?
  </td>
<td>false</td>
<td> </td>
<td>false</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>namenode</td>
<td>dfs.image.compression.codec</td>
<td>If the dfs image is compressed, how should they be compressed?
               This has to be a codec defined in io.compression.codecs.
  </td>
<td>org.apache.hadoop.io.compress.DefaultCodec</td>
<td> </td>
<td>org.apache.hadoop.io.compress.DefaultCodec</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>none</td>
<td>dfs.image.transfer.timeout</td>
<td>
        Timeout for image transfer in milliseconds. This timeout and the related
        dfs.image.transfer.bandwidthPerSec parameter should be configured such
        that normal image transfer can complete within the timeout.
        This timeout prevents client hangs when the sender fails during
        image transfer, which is particularly important during checkpointing.
        Note that this timeout applies to the entirety of image transfer, and
        is not a socket timeout.
  </td>
<td>600000</td>
<td> </td>
<td>600000</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>none</td>
<td>dfs.image.transfer.bandwidthPerSec</td>
<td>
        Maximum bandwidth used for image transfer in bytes per second.
        This can help keep normal namenode operations responsive during
        checkpointing. The maximum bandwidth and timeout in
        dfs.image.transfer.timeout should be set such that normal image
        transfers can complete successfully.
        A default value of 0 indicates that throttling is disabled. 
  </td>
<td>0</td>
<td> </td>
<td>0</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>namenode</td>
<td>dfs.namenode.support.allow.format</td>
<td>Does HDFS namenode allow itself to be formatted?
               You may consider setting this to false for any production
               cluster, to avoid any possibility of formatting a running DFS.
  </td>
<td>true</td>
<td> </td>
<td>false</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>datanode</td>
<td>dfs.datanode.max.transfer.threads</td>
<td>
        Specifies the maximum number of threads to use for transferring data
        in and out of the DN.
  </td>
<td>4096</td>
<td> </td>
<td>4096</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>datanode</td>
<td>dfs.datanode.readahead.bytes</td>
<td>
        While reading block files, if the Hadoop native libraries are available,
        the datanode can use the posix_fadvise system call to explicitly
        page data into the operating system buffer cache ahead of the current
        reader's position. This can improve performance especially when
        disks are highly contended.

        This configuration specifies the number of bytes ahead of the current
        read position which the datanode will attempt to read ahead. This
        feature may be disabled by configuring this property to 0.

        If the native libraries are not available, this configuration has no
        effect.
  </td>
<td>4193404</td>
<td> </td>
<td>4193404</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>datanode</td>
<td>dfs.datanode.drop.cache.behind.reads</td>
<td>
        In some workloads, the data read from HDFS is known to be significantly
        large enough that it is unlikely to be useful to cache it in the
        operating system buffer cache. In this case, the DataNode may be
        configured to automatically purge all data from the buffer cache
        after it is delivered to the client. This behavior is automatically
        disabled for workloads which read only short sections of a block
        (e.g HBase random-IO workloads).

        This may improve performance for some workloads by freeing buffer
        cache spage usage for more cacheable data.

        If the Hadoop native libraries are not available, this configuration
        has no effect.
  </td>
<td>false</td>
<td> </td>
<td>false</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>datanode</td>
<td>dfs.datanode.drop.cache.behind.writes</td>
<td>
        In some workloads, the data written to HDFS is known to be significantly
        large enough that it is unlikely to be useful to cache it in the
        operating system buffer cache. In this case, the DataNode may be
        configured to automatically purge all data from the buffer cache
        after it is written to disk.

        This may improve performance for some workloads by freeing buffer
        cache spage usage for more cacheable data.

        If the Hadoop native libraries are not available, this configuration
        has no effect.
  </td>
<td>false</td>
<td> </td>
<td>false</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>datanode</td>
<td>dfs.datanode.sync.behind.writes</td>
<td>
        If this configuration is enabled, the datanode will instruct the
        operating system to enqueue all written data to the disk immediately
        after it is written. This differs from the usual OS policy which
        may wait for up to 30 seconds before triggering writeback.

        This may improve performance for some workloads by smoothing the
        IO profile for data written to disk.

        If the Hadoop native libraries are not available, this configuration
        has no effect.
  </td>
<td>false</td>
<td> </td>
<td>false</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>NNHA</td>
<td>dfs.client.failover.max.attempts</td>
<td>
    Expert only. The number of client failover attempts that should be
    made before the failover is considered failed.
  </td>
<td>15</td>
<td> </td>
<td>15</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>NNHA</td>
<td>dfs.client.failover.sleep.base.millis</td>
<td>
    Expert only. The time to wait, in milliseconds, between failover
    attempts increases exponentially as a function of the number of
    attempts made so far, with a random factor of +/- 50%. This option
    specifies the base value used in the failover calculation. The
    first failover will retry immediately. The 2nd failover attempt
    will delay at least dfs.client.failover.sleep.base.millis
    milliseconds. And so on.
  </td>
<td>500</td>
<td> </td>
<td>500</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>NNHA</td>
<td>dfs.client.failover.sleep.max.millis</td>
<td>
    Expert only. The time to wait, in milliseconds, between failover
    attempts increases exponentially as a function of the number of
    attempts made so far, with a random factor of +/- 50%. This option
    specifies the maximum value to wait between failovers. 
    Specifically, the time between two failover attempts will not
    exceed +/- 50% of dfs.client.failover.sleep.max.millis
    milliseconds.
  </td>
<td>15000</td>
<td> </td>
<td>15000</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>NNHA</td>
<td>dfs.client.failover.connection.retries</td>
<td>
    Expert only. Indicates the number of retries a failover IPC client
    will make to establish a server connection.
  </td>
<td>0</td>
<td> </td>
<td>0</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>NNHA</td>
<td>dfs.client.failover.connection.retries.on.timeouts</td>
<td>
    Expert only. The number of retry attempts a failover IPC client
    will make on socket timeout when establishing a server connection.
  </td>
<td>0</td>
<td> </td>
<td>0</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>NNHA</td>
<td>dfs.nameservices</td>
<td>
    Comma-separated list of nameservices.
  </td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>NNHA</td>
<td>dfs.nameservice.id</td>
<td>
    The ID of this nameservice. If the nameservice ID is not
    configured or more than one nameservice is configured for
    dfs.nameservices it is determined automatically by
    matching the local node's address with the configured address.
  </td>
<td>null</td>
<td> </td>
<td>null</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>NNHA</td>
<td>dfs.ha.namenodes.EXAMPLENAMESERVICE</td>
<td>
    The prefix for a given nameservice, contains a comma-separated
    list of namenodes for a given nameservice (eg EXAMPLENAMESERVICE).
  </td>
<td>null</td>
<td> </td>
<td>null</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>NNHA</td>
<td>dfs.ha.namenode.id</td>
<td>
    The ID of this namenode. If the namenode ID is not configured it
    is determined automatically by matching the local node's address
    with the configured address.
  </td>
<td>null</td>
<td> </td>
<td>null</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>NNHA</td>
<td>dfs.ha.log-roll.period</td>
<td>
    How often, in seconds, the StandbyNode should ask the active to
    roll edit logs. Since the StandbyNode only reads from finalized
    log segments, the StandbyNode will only be as up-to-date as how
    often the logs are rolled. Note that failover triggers a log roll
    so the StandbyNode will be up to date before it becomes active.
  </td>
<td>120</td>
<td> </td>
<td>120</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>NNHA</td>
<td>dfs.ha.tail-edits.period</td>
<td>
    How often, in seconds, the StandbyNode should check for new
    finalized log segments in the shared edits log.
  </td>
<td>60</td>
<td> </td>
<td>60</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>NNHA</td>
<td>dfs.ha.automatic-failover.enabled</td>
<td>
    Whether automatic failover is enabled. See the HDFS High
    Availability documentation for details on automatic HA
    configuration.
  </td>
<td>false</td>
<td> </td>
<td>true</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>hdfs参数调优</td>
<td>dfs.support.append</td>
<td>
    Does HDFS allow appends to files?
  </td>
<td>true</td>
<td> </td>
<td>true</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>DNS</td>
<td>dfs.client.use.datanode.hostname</td>
<td>Whether clients should use datanode hostnames when
    connecting to datanodes.
  </td>
<td>false</td>
<td> </td>
<td>false</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>DNS</td>
<td>dfs.datanode.use.datanode.hostname</td>
<td>Whether datanodes should use datanode hostnames when
    connecting to other datanodes for data transfer.
  </td>
<td>false</td>
<td> </td>
<td>false</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>DNS</td>
<td>dfs.client.local.interfaces</td>
<td>A comma separated list of network interface names to use
    for data transfer between the client and datanodes. When creating
    a connection to read from or write to a datanode, the client
    chooses one of the specified interfaces at random and binds its
    socket to the IP of that interface. Individual names may be
    specified as either an interface name (eg "eth0"), a subinterface
    name (eg "eth0:0"), or an IP address (which may be specified using
    CIDR notation to match a range of IPs).
  </td>
<td>null</td>
<td> </td>
<td>null</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>安全</td>
<td>dfs.namenode.kerberos.internal.spnego.principal</td>
<td>null</td>
<td>${dfs.web.authentication.kerberos.principal}</td>
<td> </td>
<td>${dfs.web.authentication.kerberos.principal}</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>安全</td>
<td>dfs.secondary.namenode.kerberos.internal.spnego.principal</td>
<td>null</td>
<td>${dfs.web.authentication.kerberos.principal}</td>
<td> </td>
<td>${dfs.web.authentication.kerberos.principal}</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>staleDataNode</td>
<td>dfs.namenode.avoid.read.stale.datanode</td>
<td>
    Indicate whether or not to avoid reading from "stale" datanodes whose
    heartbeat messages have not been received by the namenode 
    for more than a specified time interval. Stale datanodes will be
    moved to the end of the node list returned for reading. See
    dfs.namenode.avoid.write.stale.datanode for a similar setting for writes.
  </td>
<td>false</td>
<td> </td>
<td>false</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>staleDataNode</td>
<td>dfs.namenode.avoid.write.stale.datanode</td>
<td>
    Indicate whether or not to avoid writing to "stale" datanodes whose 
    heartbeat messages have not been received by the namenode 
    for more than a specified time interval. Writes will avoid using 
    stale datanodes unless more than a configured ratio 
    (dfs.namenode.write.stale.datanode.ratio) of datanodes are marked as 
    stale. See dfs.namenode.avoid.read.stale.datanode for a similar setting
    for reads.
  </td>
<td>false</td>
<td> </td>
<td>false</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>staleDataNode</td>
<td>dfs.namenode.stale.datanode.interval</td>
<td>
    Default time interval for marking a datanode as "stale", i.e., if 
    the namenode has not received heartbeat msg from a datanode for 
    more than this time interval, the datanode will be marked and treated 
    as "stale" by default. The stale interval cannot be too small since 
    otherwise this may cause too frequent change of stale states. 
    We thus set a minimum stale interval value (the default value is 3 times 
    of heartbeat interval) and guarantee that the stale interval cannot be less
    than the minimum value.
  </td>
<td>30000</td>
<td> </td>
<td>30000</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>staleDataNode</td>
<td>dfs.namenode.write.stale.datanode.ratio</td>
<td>
    When the ratio of number stale datanodes to total datanodes marked
    is greater than this ratio, stop avoiding writing to stale nodes so
    as to prevent causing hotspots.
  </td>
<td>0.5f</td>
<td> </td>
<td>0.5f</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>namenode</td>
<td>dfs.namenode.invalidate.work.pct.per.iteration</td>
<td>
    *Note*: Advanced property. Change with caution.
    This determines the percentage amount of block
    invalidations (deletes) to do over a single DN heartbeat
    deletion command. The final deletion count is determined by applying this
    percentage to the number of live nodes in the system.
    The resultant number is the number of blocks from the deletion list
    chosen for proper invalidation over a single heartbeat of a single DN.
    Value should be a positive, non-zero percentage in float notation (X.Yf),
    with 1.0f meaning 100%.
  </td>
<td>0.32f</td>
<td> </td>
<td>0.32f</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>namenode</td>
<td>dfs.namenode.replication.work.multiplier.per.iteration</td>
<td>
    *Note*: Advanced property. Change with caution.
    This determines the total amount of block transfers to begin in
    parallel at a DN, for replication, when such a command list is being
    sent over a DN heartbeat by the NN. The actual number is obtained by
    multiplying this multiplier with the total number of live nodes in the
    cluster. The result number is the number of blocks to begin transfers
    immediately for, per DN heartbeat. This number can be any positive,
    non-zero integer.
  </td>
<td>2</td>
<td> </td>
<td>2</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>webhdfs</td>
<td>dfs.webhdfs.enabled</td>
<td>
    Enable WebHDFS (REST API) in Namenodes and Datanodes.
  </td>
<td>false</td>
<td> </td>
<td>false</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>fuse</td>
<td>hadoop.fuse.connection.timeout</td>
<td>
    The minimum number of seconds that we'll cache libhdfs connection objects
    in fuse_dfs. Lower values will result in lower memory consumption; higher
    values may speed up access by avoiding the overhead of creating new
    connection objects.
  </td>
<td>300</td>
<td> </td>
<td>300</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>fuse</td>
<td>hadoop.fuse.timer.period</td>
<td>
    The number of seconds between cache expiry checks in fuse_dfs. Lower values
    will result in fuse_dfs noticing changes to Kerberos ticket caches more
    quickly.
  </td>
<td>5</td>
<td> </td>
<td>5</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>日志</td>
<td>dfs.metrics.percentiles.intervals</td>
<td>
    Comma-delimited set of integers denoting the desired rollover intervals 
    (in seconds) for percentile latency metrics on the Namenode and Datanode.
    By default, percentile latency metrics are disabled.
  </td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>安全</td>
<td>dfs.encrypt.data.transfer</td>
<td>
    Whether or not actual block data that is read/written from/to HDFS should
    be encrypted on the wire. This only needs to be set on the NN and DNs,
    clients will deduce this automatically.
  </td>
<td>false</td>
<td> </td>
<td>false</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>安全</td>
<td>dfs.encrypt.data.transfer.algorithm</td>
<td>
    This value may be set to either "3des" or "rc4". If nothing is set, then
    the configured JCE default on the system is used (usually 3DES.) It is
    widely believed that 3DES is more cryptographically secure, but RC4 is
    substantially faster.
  </td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>none</td>
<td>dfs.datanode.hdfs-blocks-metadata.enabled</td>
<td>
    Boolean which enables backend datanode-side support for the experimental DistributedFileSystem#getFileVBlockStorageLocations API.
  </td>
<td>true</td>
<td> </td>
<td>true</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>none</td>
<td>dfs.client.file-block-storage-locations.num-threads</td>
<td>
    Number of threads used for making parallel RPCs in DistributedFileSystem#getFileBlockStorageLocations().
  </td>
<td>10</td>
<td> </td>
<td>10</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>none</td>
<td>dfs.client.file-block-storage-locations.timeout</td>
<td>
    Timeout (in seconds) for the parallel RPCs made in DistributedFileSystem#getFileBlockStorageLocations().
  </td>
<td>60</td>
<td> </td>
<td>60</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>IP端口</td>
<td>dfs.journalnode.rpc-address</td>
<td>
    The JournalNode RPC server address and port.
  </td>
<td>0.0.0.0:8485</td>
<td> </td>
<td>0.0.0.0:8485</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>IP端口</td>
<td>dfs.journalnode.http-address</td>
<td>
    The address and port the JournalNode web UI listens on.
    If the port is 0 then the server will start on a free port.
  </td>
<td>0.0.0.0:8480</td>
<td> </td>
<td>0.0.0.0:8480</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>日志</td>
<td>dfs.namenode.audit.loggers</td>
<td>
    List of classes implementing audit loggers that will receive audit events.
    These should be implementations of org.apache.hadoop.hdfs.server.namenode.AuditLogger.
    The special value "default" can be used to reference the default audit
    logger, which uses the configured log system. Installing custom audit loggers
    may affect the performance and stability of the NameNode. Refer to the custom
    logger's documentation for more details.
  </td>
<td>default</td>
<td> </td>
<td>default</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>本地目录</td>
<td>dfs.domain.socket.path</td>
<td>
    Optional.  This is a path to a UNIX domain socket that will be used for
    communication between the DataNode and local HDFS clients.
    If the string "_PORT" is present in this path, it will be replaced by the
    TCP port of the DataNode.
  </td>
<td>/var/run/hadoop-hdfs/dn._PORT</td>
<td> </td>
<td>/var/run/hadoop-hdfs/dn._PORT</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>datanode</td>
<td>dfs.datanode.available-space-volume-choosing-policy.balanced-space-threshold</td>
<td>
    Only used when the dfs.datanode.fsdataset.volume.choosing.policy is set to
    org.apache.hadoop.hdfs.server.datanode.fsdataset.AvailableSpaceVolumeChoosingPolicy.
    This setting controls how much DN volumes are allowed to differ in terms of
    bytes of free disk space before they are considered imbalanced. If the free
    space of all the volumes are within this range of each other, the volumes
    will be considered balanced and block assignments will be done on a pure
    round robin basis.
  </td>
<td>10737418240</td>
<td> </td>
<td>10737418240</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>hdfs-default.xml</td>
<td>datanode</td>
<td>dfs.datanode.available-space-volume-choosing-policy.balanced-space-preference-fraction</td>
<td>
    Only used when the dfs.datanode.fsdataset.volume.choosing.policy is set to
    org.apache.hadoop.hdfs.server.datanode.fsdataset.AvailableSpaceVolumeChoosingPolicy.
    This setting controls what percentage of new block allocations will be sent
    to volumes with more available disk space than others. This setting should
    be in the range 0.0 - 1.0, though in practice 0.5 - 1.0, since there should
    be no reason to prefer that volumes with less available disk space receive
    more block allocations.
  </td>
<td>0.75f</td>
<td> </td>
<td>0.75f</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>httpfs-default.xml</td>
<td>httpfs</td>
<td>httpfs.buffer.size</td>
<td>
      The buffer size used by a read/write request when streaming data from/to
      HDFS.
    </td>
<td>4096</td>
<td> </td>
<td>4096</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>httpfs-default.xml</td>
<td>httpfs</td>
<td>httpfs.services</td>
<td>
      Services used by the httpfs server.
    </td>
<td>
      org.apache.hadoop.lib.service.instrumentation.InstrumentationService,
      org.apache.hadoop.lib.service.scheduler.SchedulerService,
      org.apache.hadoop.lib.service.security.GroupsService,
      org.apache.hadoop.lib.service.security.ProxyUserService,
      org.apache.hadoop.lib.service.security.DelegationTokenManagerService,
      org.apache.hadoop.lib.service.hadoop.FileSystemAccessService
    </td>
<td> </td>
<td>
      org.apache.hadoop.lib.service.instrumentation.InstrumentationService,
      org.apache.hadoop.lib.service.scheduler.SchedulerService,
      org.apache.hadoop.lib.service.security.GroupsService,
      org.apache.hadoop.lib.service.security.ProxyUserService,
      org.apache.hadoop.lib.service.security.DelegationTokenManagerService,
      org.apache.hadoop.lib.service.hadoop.FileSystemAccessService
    </td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>httpfs-default.xml</td>
<td>httpfs</td>
<td>kerberos.realm</td>
<td>
      Kerberos realm, used only if Kerberos authentication is used between
      the clients and httpfs or between HttpFS and HDFS.

      This property is only used to resolve other properties within this
      configuration file.
    </td>
<td>LOCALHOST</td>
<td> </td>
<td>LOCALHOST</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>httpfs-default.xml</td>
<td>httpfs</td>
<td>httpfs.hostname</td>
<td>
      Property used to synthetize the HTTP Kerberos principal used by httpfs.

      This property is only used to resolve other properties within this
      configuration file.
    </td>
<td>${httpfs.http.hostname}</td>
<td> </td>
<td>${httpfs.http.hostname}</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>httpfs-default.xml</td>
<td>httpfs</td>
<td>httpfs.authentication.signature.secret.file</td>
<td>
      File containing the secret to sign HttpFS hadoop-auth cookies.

      This file should be readable only by the system user running HttpFS service.

      If multiple HttpFS servers are used in a load-balancer/round-robin fashion,
      they should share the secret file.
    </td>
<td>${httpfs.config.dir}/httpfs-signature.secret</td>
<td> </td>
<td>${httpfs.config.dir}/httpfs-signature.secret</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>httpfs-default.xml</td>
<td>httpfs</td>
<td>httpfs.authentication.type</td>
<td>
      Defines the authentication mechanism used by httpfs for its HTTP clients.

      Valid values are 'simple' or 'kerberos'.

      If using 'simple' HTTP clients must specify the username with the
      'user.name' query string parameter.

      If using 'kerberos' HTTP clients must use HTTP SPNEGO or delegation tokens.
    </td>
<td>simple</td>
<td> </td>
<td>simple</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>httpfs-default.xml</td>
<td>httpfs</td>
<td>httpfs.authentication.kerberos.principal</td>
<td>
      The HTTP Kerberos principal used by HttpFS in the HTTP endpoint.

      The HTTP Kerberos principal MUST start with 'HTTP/' per Kerberos
      HTTP SPNEGO specification.
    </td>
<td>HTTP/${httpfs.hostname}@${kerberos.realm}</td>
<td> </td>
<td>HTTP/${httpfs.hostname}@${kerberos.realm}</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>httpfs-default.xml</td>
<td>httpfs</td>
<td>httpfs.authentication.kerberos.keytab</td>
<td>
      The Kerberos keytab file with the credentials for the
      HTTP Kerberos principal used by httpfs in the HTTP endpoint.
    </td>
<td>${user.home}/httpfs.keytab</td>
<td> </td>
<td>${user.home}/httpfs.keytab</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>httpfs-default.xml</td>
<td>httpfs</td>
<td>httpfs.proxyuser.#USER#.hosts</td>
<td>
      List of hosts the '#USER#' user is allowed to perform 'doAs'
      operations.

      The '#USER#' must be replaced with the username o the user who is
      allowed to perform 'doAs' operations.

      The value can be the '*' wildcard or a list of hostnames.

      For multiple users copy this property and replace the user name
      in the property name.
    </td>
<td>*</td>
<td> </td>
<td>*</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>httpfs-default.xml</td>
<td>httpfs</td>
<td>httpfs.proxyuser.#USER#.groups</td>
<td>
      List of groups the '#USER#' user is allowed to impersonate users
      from to perform 'doAs' operations.

      The '#USER#' must be replaced with the username o the user who is
      allowed to perform 'doAs' operations.

      The value can be the '*' wildcard or a list of groups.

      For multiple users copy this property and replace the user name
      in the property name.
    </td>
<td>*</td>
<td> </td>
<td>*</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>httpfs-default.xml</td>
<td>httpfs</td>
<td>httpfs.delegation.token.manager.update.interval</td>
<td>
      HttpFS delegation token update interval, default 1 day, in seconds.
    </td>
<td>86400</td>
<td> </td>
<td>86400</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>httpfs-default.xml</td>
<td>httpfs</td>
<td>httpfs.delegation.token.manager.max.lifetime</td>
<td>
      HttpFS delegation token maximum lifetime, default 7 days, in seconds
    </td>
<td>604800</td>
<td> </td>
<td>604800</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>httpfs-default.xml</td>
<td>httpfs</td>
<td>httpfs.delegation.token.manager.renewal.interval</td>
<td>
      HttpFS delegation token update interval, default 1 day, in seconds.
    </td>
<td>86400</td>
<td> </td>
<td>86400</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>httpfs-default.xml</td>
<td>httpfs</td>
<td>httpfs.hadoop.authentication.type</td>
<td>
      Defines the authentication mechanism used by httpfs to connect to
      the HDFS Namenode.

      Valid values are 'simple' and 'kerberos'.
    </td>
<td>simple</td>
<td> </td>
<td>simple</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>httpfs-default.xml</td>
<td>httpfs</td>
<td>httpfs.hadoop.authentication.kerberos.keytab</td>
<td>
      The Kerberos keytab file with the credentials for the
      Kerberos principal used by httpfs to connect to the HDFS Namenode.
    </td>
<td>${user.home}/httpfs.keytab</td>
<td> </td>
<td>${user.home}/httpfs.keytab</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>httpfs-default.xml</td>
<td>httpfs</td>
<td>httpfs.hadoop.authentication.kerberos.principal</td>
<td>
      The Kerberos principal used by httpfs to connect to the HDFS Namenode.
    </td>
<td>${user.name}/${httpfs.hostname}@${kerberos.realm}</td>
<td> </td>
<td>${user.name}/${httpfs.hostname}@${kerberos.realm}</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>httpfs-default.xml</td>
<td>httpfs</td>
<td>httpfs.hadoop.filesystem.cache.purge.frequency</td>
<td>
      Frequency, in seconds, for the idle filesystem purging daemon runs.
    </td>
<td>60</td>
<td> </td>
<td>60</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>httpfs-default.xml</td>
<td>httpfs</td>
<td>httpfs.hadoop.filesystem.cache.purge.timeout</td>
<td>
      Timeout, in seconds, for an idle filesystem to be purged.
    </td>
<td>60</td>
<td> </td>
<td>60</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>httpfs-default.xml</td>
<td>httpfs</td>
<td>httpfs.user.provider.user.pattern</td>
<td>
      Valid pattern for user and group names, it must be a valid java regex.
    </td>
<td>^[A-Za-z_][A-Za-z0-9._-]*[$]?$</td>
<td> </td>
<td>^[A-Za-z_][A-Za-z0-9._-]*[$]?$</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>jobtracker</td>
<td>mapreduce.jobtracker.jobhistory.location</td>
<td> If job tracker is static the history files are stored 
  in this single well known place. If No value is set here, by default,
  it is in the local file system at ${hadoop.log.dir}/history.
  </td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>jobtracker</td>
<td>mapreduce.jobtracker.jobhistory.task.numberprogresssplits</td>
<td> Every task attempt progresses from 0.0 to 1.0 [unless
  it fails or is killed].  We record, for each task attempt, certain 
  statistics over each twelfth of the progress range.  You can change
  the number of intervals we divide the entire range of progress into
  by setting this property.  Higher values give more precision to the
  recorded data, but costs more memory in the job tracker at runtime.
  Each increment in this attribute costs 16 bytes per running task.
  </td>
<td>12</td>
<td> </td>
<td>12</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>none</td>
<td>mapreduce.job.userhistorylocation</td>
<td> User can specify a location to store the history files of 
  a particular job. If nothing is specified, the logs are stored in 
  output directory. The files are stored in "_logs/history/" in the directory.
  User can stop logging by giving the value "none". 
  </td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>hadoop.log.dir</td>
<td>mapreduce.jobtracker.jobhistory.completed.location</td>
<td> The completed job history files are stored at this single well 
  known location. If nothing is specified, the files are stored at 
  ${mapreduce.jobtracker.jobhistory.location}/done.
  </td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>job</td>
<td>mapreduce.job.committer.setup.cleanup.needed</td>
<td> true, if job needs job-setup and job-cleanup.
                false, otherwise  
  </td>
<td>true</td>
<td> </td>
<td>true</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>job</td>
<td>mapreduce.task.io.sort.factor</td>
<td>The number of streams to merge at once while sorting
  files.  This determines the number of open file handles.</td>
<td>10</td>
<td> </td>
<td>20</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>job</td>
<td>mapreduce.task.io.sort.mb</td>
<td>The total amount of buffer memory to use while sorting 
  files, in megabytes.  By default, gives each merge stream 1MB, which
  should minimize seeks.</td>
<td>100</td>
<td> </td>
<td>200</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>job</td>
<td>mapreduce.map.sort.spill.percent</td>
<td>The soft limit in the serialization buffer. Once reached, a
  thread will begin to spill the contents to disk in the background. Note that
  collection will not block if this threshold is exceeded while a spill is
  already in progress, so spills may be larger than this threshold when it is
  set to less than .5</td>
<td>0.80</td>
<td> </td>
<td>0.80</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>jobtracker</td>
<td>mapreduce.jobtracker.address</td>
<td>The host and port that the MapReduce job tracker runs
  at.  If "local", then jobs are run in-process as a single map
  and reduce task.
  </td>
<td>local</td>
<td> </td>
<td>local</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>job</td>
<td>mapreduce.local.clientfactory.class.name</td>
<td>This the client factory that is responsible for 
  creating local job runner client</td>
<td>org.apache.hadoop.mapred.LocalClientFactory</td>
<td> </td>
<td>org.apache.hadoop.mapred.LocalClientFactory</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>IP端口</td>
<td>mapreduce.jobtracker.http.address</td>
<td>
    The job tracker http server address and port the server will listen on.
    If the port is 0 then the server will start on a free port.
  </td>
<td>0.0.0.0:50030</td>
<td> </td>
<td>0.0.0.0:50030</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>jobtracker</td>
<td>mapreduce.jobtracker.handler.count</td>
<td>
    The number of server threads for the JobTracker. This should be roughly
    4% of the number of tasktracker nodes.
  </td>
<td>10</td>
<td> </td>
<td>10</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>IP端口</td>
<td>mapreduce.tasktracker.report.address</td>
<td>The interface and port that task tracker server listens on. 
  Since it is only connected to by the tasks, it uses the local interface.
  EXPERT ONLY. Should only be changed if your host does not have the loopback 
  interface.</td>
<td>127.0.0.1:0</td>
<td> </td>
<td>127.0.0.1:0</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>本地目录</td>
<td>mapreduce.cluster.local.dir</td>
<td>The local directory where MapReduce stores intermediate
  data files.  May be a comma-separated list of
  directories on different devices in order to spread disk i/o.
  Directories that do not exist are ignored.
  </td>
<td>${hadoop.tmp.dir}/mapred/local</td>
<td> </td>
<td>${hadoop.tmp.dir}/mapred/local</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>本地目录</td>
<td>mapreduce.jobtracker.system.dir</td>
<td>The directory where MapReduce stores control files.
YARN中不适用
  </td>
<td>${hadoop.tmp.dir}/mapred/system</td>
<td> </td>
<td>${hadoop.tmp.dir}/mapred/system</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>本地目录</td>
<td>mapreduce.jobtracker.staging.root.dir</td>
<td>The root of the staging area for users' job files
  In practice, this should be the directory where users' home 
  directories are located (usually /user)
  YARN中不适用
  </td>
<td>${hadoop.tmp.dir}/mapred/staging</td>
<td> </td>
<td>${hadoop.tmp.dir}/mapred/staging</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>本地目录</td>
<td>mapreduce.cluster.temp.dir</td>
<td>A shared directory for temporary files.
YARN中不适用
  </td>
<td>${hadoop.tmp.dir}/mapred/temp</td>
<td> </td>
<td>${hadoop.tmp.dir}/mapred/temp</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>tasktracker</td>
<td>mapreduce.tasktracker.local.dir.minspacestart</td>
<td>If the space in mapreduce.cluster.local.dir drops under this, 
  do not ask for more tasks.
  Value in bytes.
  YARN中不适用
  </td>
<td>0</td>
<td> </td>
<td>0</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>tasktracker</td>
<td>mapreduce.tasktracker.local.dir.minspacekill</td>
<td>If the space in mapreduce.cluster.local.dir drops under this, 
    do not ask more tasks until all the current ones have finished and 
    cleaned up. Also, to save the rest of the tasks we have running, 
    kill one of them, to clean up some space. Start with the reduce tasks,
    then go with the ones that have finished the least.
    Value in bytes.
  </td>
<td>0</td>
<td> </td>
<td>0</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>jobtracker</td>
<td>mapreduce.jobtracker.expire.trackers.interval</td>
<td>Expert: The time-interval, in miliseconds, after which
  a tasktracker is declared 'lost' if it doesn't send heartbeats.
  </td>
<td>600000</td>
<td> </td>
<td>600000</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>tasktracker</td>
<td>mapreduce.tasktracker.instrumentation</td>
<td>Expert: The instrumentation class to associate with each TaskTracker.
  </td>
<td>org.apache.hadoop.mapred.TaskTrackerMetricsInst</td>
<td> </td>
<td>org.apache.hadoop.mapred.TaskTrackerMetricsInst</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>tasktracker</td>
<td>mapreduce.tasktracker.resourcecalculatorplugin</td>
<td>
   Name of the class whose instance will be used to query resource information
   on the tasktracker.
   
   The class must be an instance of 
   org.apache.hadoop.util.ResourceCalculatorPlugin. If the value is null, the
   tasktracker attempts to use a class appropriate to the platform. 
   Currently, the only platform supported is Linux.
  </td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>tasktracker</td>
<td>mapreduce.tasktracker.taskmemorymanager.monitoringinterval</td>
<td>The interval, in milliseconds, for which the tasktracker waits
   between two cycles of monitoring its tasks' memory usage. Used only if
   tasks' memory management is enabled via mapred.tasktracker.tasks.maxmemory.
   </td>
<td>5000</td>
<td> </td>
<td>5000</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>tasktracker</td>
<td>mapreduce.tasktracker.tasks.sleeptimebeforesigkill</td>
<td>The time, in milliseconds, the tasktracker waits for sending a
  SIGKILL to a task, after it has been sent a SIGTERM. This is currently
  not used on WINDOWS where tasks are just sent a SIGTERM.
  </td>
<td>5000</td>
<td> </td>
<td>5000</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>job</td>
<td>mapreduce.job.maps</td>
<td>The default number of map tasks per job.
  Ignored when mapreduce.jobtracker.address is "local".  
  对于某些特定的inputformat 还是适用
  </td>
<td>2</td>
<td> </td>
<td>2</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>job</td>
<td>mapreduce.job.reduces</td>
<td>The default number of reduce tasks per job. Typically set to 99%
  of the cluster's reduce capacity, so that if a node fails the reduces can 
  still be executed in a single wave.
  Ignored when mapreduce.jobtracker.address is "local".
  </td>
<td>1</td>
<td> </td>
<td>1</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>jobtracker</td>
<td>mapreduce.jobtracker.restart.recover</td>
<td>"true" to enable (job) recovery upon restart,
               "false" to start afresh
  </td>
<td>false</td>
<td> </td>
<td>false</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>jobtracker</td>
<td>mapreduce.jobtracker.jobhistory.block.size</td>
<td>The block size of the job history file. Since the job recovery
               uses job history, its important to dump job history to disk as 
               soon as possible. Note that this is an expert level parameter.
               The default value is set to 3 MB.
  </td>
<td>3145728</td>
<td> </td>
<td>3145728</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>jobtracker</td>
<td>mapreduce.jobtracker.taskscheduler</td>
<td>The class responsible for scheduling the tasks.</td>
<td>org.apache.hadoop.mapred.JobQueueTaskScheduler</td>
<td> </td>
<td>org.apache.hadoop.mapred.JobQueueTaskScheduler</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>job</td>
<td>mapreduce.job.split.metainfo.maxsize</td>
<td>The maximum permissible size of the split metainfo file. 
  The JobTracker won't attempt to read split metainfo files bigger than
  the configured value.
  No limits if set to -1.
  </td>
<td>10000000</td>
<td> </td>
<td>10000000</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>jobtracker</td>
<td>mapreduce.jobtracker.taskscheduler.maxrunningtasks.perjob</td>
<td>The maximum number of running tasks for a job before
  it gets preempted. No limits if undefined.
  </td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>job</td>
<td>mapreduce.map.maxattempts</td>
<td>Expert: The maximum number of attempts per map task.
  In other words, framework will try to execute a map task these many number
  of times before giving up on it.
  map重试次数
  </td>
<td>4</td>
<td> </td>
<td>4</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>job</td>
<td>mapreduce.reduce.maxattempts</td>
<td>Expert: The maximum number of attempts per reduce task.
  In other words, framework will try to execute a reduce task these many number
  of times before giving up on it.
  reduce重试次数
  </td>
<td>4</td>
<td> </td>
<td>4</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>job</td>
<td>mapreduce.reduce.shuffle.retry-delay.max.ms</td>
<td>The maximum number of ms the reducer will delay before retrying
  to download map data.
  reduce重新下载map的数据的延迟时间
  </td>
<td>60000</td>
<td> </td>
<td>60000</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>job</td>
<td>mapreduce.reduce.shuffle.parallelcopies</td>
<td>The default number of parallel transfers run by reduce
  during the copy(shuffle) phase.
  copy阶段的reduce的传输并发数量
  </td>
<td>5</td>
<td> </td>
<td>5</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>job</td>
<td>mapreduce.reduce.shuffle.connect.timeout</td>
<td>Expert: The maximum amount of time (in milli seconds) reduce
  task spends in trying to connect to a tasktracker for getting map output.
  shuffle连接超时时长
  </td>
<td>180000</td>
<td> </td>
<td>180000</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>job</td>
<td>mapreduce.reduce.shuffle.read.timeout</td>
<td>Expert: The maximum amount of time (in milli seconds) reduce
  task waits for map output data to be available for reading after obtaining
  connection.
  shuffle读取超时时长
  </td>
<td>180000</td>
<td> </td>
<td>180000</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>job</td>
<td>mapreduce.task.timeout</td>
<td>The number of milliseconds before a task will be
  terminated if it neither reads an input, writes an output, nor
  updates its status string.  A value of 0 disables the timeout.
  task假死杀死时间
  </td>
<td>600000</td>
<td> </td>
<td>600000</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>tasktracker</td>
<td>mapreduce.tasktracker.map.tasks.maximum</td>
<td>The maximum number of map tasks that will be run
  simultaneously by a task tracker.
  </td>
<td>2</td>
<td> </td>
<td>2</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>tasktracker</td>
<td>mapreduce.tasktracker.reduce.tasks.maximum</td>
<td>The maximum number of reduce tasks that will be run
  simultaneously by a task tracker.
  </td>
<td>2</td>
<td> </td>
<td>2</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>jobtracker</td>
<td>mapreduce.jobtracker.retiredjobs.cache.size</td>
<td>The number of retired job status to keep in the cache.
  </td>
<td>1000</td>
<td> </td>
<td>1000</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>tasktracker</td>
<td>mapreduce.tasktracker.outofband.heartbeat</td>
<td>Expert: Set this to true to let the tasktracker send an 
  out-of-band heartbeat on task-completion for better latency.
  </td>
<td>false</td>
<td> </td>
<td>false</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>jobtracker</td>
<td>mapreduce.jobtracker.jobhistory.lru.cache.size</td>
<td>The number of job history files loaded in memory. The jobs are 
  loaded when they are first accessed. The cache is cleared based on LRU.
  </td>
<td>5</td>
<td> </td>
<td>5</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>jobtracker</td>
<td>mapreduce.jobtracker.instrumentation</td>
<td>Expert: The instrumentation class to associate with each JobTracker.
  </td>
<td>org.apache.hadoop.mapred.JobTrackerMetricsInst</td>
<td> </td>
<td>org.apache.hadoop.mapred.JobTrackerMetricsInst</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>job</td>
<td>mapred.child.java.opts</td>
<td>Java opts for the task tracker child processes.  
  The following symbol, if present, will be interpolated: @taskid@ is replaced 
  by current TaskID. Any other occurrences of '@' will go unchanged.
  For example, to enable verbose gc logging to a file named for the taskid in
  /tmp and to set the heap maximum to be a gigabyte, pass a 'value' of:
        -Xmx1024m -verbose:gc -Xloggc:/tmp/@taskid@.gc
  
  Usage of -Djava.library.path can cause programs to no longer function if
  hadoop native libraries are used. These values should instead be set as part 
  of LD_LIBRARY_PATH in the map / reduce JVM env using the mapreduce.map.env and 
  mapreduce.reduce.env config settings. 
  过时配置child环境变量
  详情参考mapreduce.map.java.opts和mapreduce.reduce.java.opts
  </td>
<td>-Xmx200m</td>
<td> </td>
<td>-Xmx200m</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>job</td>
<td>mapred.child.env</td>
<td>User added environment variables for the task tracker child 
  processes. Example :
  1) A=foo  This will set the env variable A to foo
  2) B=$B:c This is inherit tasktracker's B env variable.  
  过时配置child环境变量
  </td>
<td>null</td>
<td> </td>
<td>null</td>
<td>I9</td>
</tr>

<tr>
<td>cdh4.3.0</td>
<td>MRJobConfig</td>
<td>job</td>
<td>mapreduce.map.memory.mb</td>
<td>map阶段申请的内存
  </td>
<td>null</td>
<td> </td>
<td>640M</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>MRJobConfig</td>
<td>job</td>
<td>mapreduce.reduce.memory.mb</td>
<td>reduce阶段申请的内存
  </td>
<td>null</td>
<td> </td>
<td>640M</td>
<td>I9</td>
</tr>

<tr>
<td>cdh4.3.0</td>
<td>MRJobConfig</td>
<td>job</td>
<td>mapreduce.map.java.opts</td>
<td>map阶段的启动参数，此处设置的最大堆的内存必须要比，申请的内存少
  </td>
<td>null</td>
<td> </td>
<td>-Xmx400M</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>MRJobConfig</td>
<td>job</td>
<td>mapreduce.reduce.java.opts</td>
<td>map阶段的启动参数，此处设置的最大堆的内存必须要比，申请的内存少
  </td>
<td>null</td>
<td> </td>
<td>-Xmx400M</td>
<td>I9</td>
</tr>

<tr>
<td>cdh4.3.0</td>
<td>MRJobConfig</td>
<td>job</td>
<td>mapreduce.admin.map.child.java.opts</td>
<td>默认的admin配置的map启动参数，优先级比mapreduce.map.java.opts低
  </td>
<td>null</td>
<td> </td>
<td>-Xmx400M</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>MRJobConfig</td>
<td>job</td>
<td>mapreduce.admin.reduce.child.java.opts</td>
<td>默认的admin配置的reduce启动参数，优先级比mapreduce.reduce.java.opts低
  </td>
<td>null</td>
<td> </td>
<td>-Xmx400M</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>MRJobConfig</td>
<td>job</td>
<td>mapreduce.reduce.env</td>
<td>map启动的环境变量
  </td>
<td>null</td>
<td> </td>
<td>-Xmx400M</td>
<td>I5/td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>MRJobConfig</td>
<td>job</td>
<td>mapreduce.map.env</td>
<td>reduce启动的环境变量
  </td>
<td>null</td>
<td> </td>
<td>-Xmx400M</td>
<td>I5</td>
</tr>

<tr>
<td>cdh4.3.0</td>
<td>MRJobConfig</td>
<td>job</td>
<td>mapreduce.job.counters.group.name.max</td>
<td>counter的组上限
  </td>
<td>128</td>
<td> </td>
<td>128</td>
<td>I1</td>
</tr>

<tr>
<td>cdh4.3.0</td>
<td>MRJobConfig</td>
<td>job</td>
<td>mapreduce.job.counters.counter.name.max</td>
<td>counter的名字上限
  </td>
<td>64</td>
<td> </td>
<td>64</td>
<td>I1</td>
</tr>

<tr>
<td>cdh4.3.0</td>
<td>MRJobConfig</td>
<td>job</td>
<td>mapreduce.job.counters.groups.max</td>
<td>counters组上限
  </td>
<td>64</td>
<td> </td>
<td>64</td>
<td>I1</td>
</tr>

<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>job</td>
<td>mapreduce.admin.user.env</td>
<td>Expert: Additional execution environment entries for 
  map and reduce task processes. This is not an additive property.
  You must preserve the original value if you want your map and
  reduce tasks to have access to native libraries (compression, etc). 
  </td>
<td>LD_LIBRARY_PATH=$HADOOP_COMMON_HOME/lib/native</td>
<td> </td>
<td>LD_LIBRARY_PATH=$HADOOP_COMMON_HOME/lib/native</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>job</td>
<td>mapreduce.task.tmp.dir</td>
<td> To set the value of tmp directory for map and reduce tasks.
  If the value is an absolute path, it is directly assigned. Otherwise, it is
  prepended with task's working directory. The java tasks are executed with
  option -Djava.io.tmpdir='the absolute path of the tmp dir'. Pipes and
  streaming are set with environment variable,
   TMPDIR='the absolute path of the tmp dir'
  </td>
<td>./tmp</td>
<td> </td>
<td>./tmp</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>日志</td>
<td>mapreduce.map.log.level</td>
<td>The logging level for the map task. The allowed levels are:
  OFF, FATAL, ERROR, WARN, INFO, DEBUG, TRACE and ALL.
  </td>
<td>INFO</td>
<td> </td>
<td>INFO</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>日志</td>
<td>mapreduce.reduce.log.level</td>
<td>The logging level for the reduce task. The allowed levels are:
  OFF, FATAL, ERROR, WARN, INFO, DEBUG, TRACE and ALL.
  </td>
<td>INFO</td>
<td> </td>
<td>INFO</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>job</td>
<td>mapreduce.reduce.merge.inmem.threshold</td>
<td>The threshold, in terms of the number of files 
  for the in-memory merge process. When we accumulate threshold number of files
  we initiate the in-memory merge and spill to disk. A value of 0 or less than
  0 indicates we want to DON'T have any threshold and instead depend only on
  the ramfs's memory consumption to trigger the merge.
  内存中进行合并的文件数量
  </td>
<td>1000</td>
<td> </td>
<td>1000</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>reduce</td>
<td>mapreduce.reduce.shuffle.merge.percent</td>
<td>The usage threshold at which an in-memory merge will be
  initiated, expressed as a percentage of the total memory allocated to
  storing in-memory map outputs, as defined by
  mapreduce.reduce.shuffle.input.buffer.percent.
  reduce的shuffle内存使用总量中用于保存map阶段输出的内存量
  </td>
<td>0.66</td>
<td> </td>
<td>0.66</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>reduce</td>
<td>mapreduce.reduce.shuffle.input.buffer.percent</td>
<td>The percentage of memory to be allocated from the maximum heap
  size to storing map outputs during the shuffle.
  reduce的shuffle内存使用总量
  </td>
<td>0.70</td>
<td> </td>
<td>0.70</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>reduce</td>
<td>mapreduce.reduce.input.buffer.percent</td>
<td>The percentage of memory- relative to the maximum heap size- to
  retain map outputs during the reduce. When the shuffle is concluded, any
  remaining map outputs in memory must consume less than this threshold before
  the reduce can begin.
  
  </td>
<td>0.0</td>
<td> </td>
<td>0.0</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>reduce</td>
<td>mapreduce.reduce.shuffle.memory.limit.percent</td>
<td>Expert: Maximum percentage of the in-memory limit that a
  single shuffle can consume
  单一的shuffle内存使用量
  </td>
<td>0.25</td>
<td> </td>
<td>0.25</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>安全</td>
<td>mapreduce.shuffle.ssl.enabled</td>
<td>
    Whether to use SSL for for the Shuffle HTTP endpoints.
  </td>
<td>false</td>
<td> </td>
<td>false</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>reduce</td>
<td>mapreduce.shuffle.ssl.file.buffer.size</td>
<td>Buffer size for reading spills from file when using SSL.
  </td>
<td>65536</td>
<td> </td>
<td>65536</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>reduce</td>
<td>mapreduce.reduce.markreset.buffer.percent</td>
<td>The percentage of memory -relative to the maximum heap size- to
  be used for caching values when using the mark-reset functionality.
  </td>
<td>0.0</td>
<td> </td>
<td>0.0</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>speculative</td>
<td>mapreduce.map.speculative</td>
<td>If true, then multiple instances of some map tasks 
               may be executed in parallel.</td>
<td>true</td>
<td> </td>
<td>true</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>speculative</td>
<td>mapreduce.reduce.speculative</td>
<td>If true, then multiple instances of some reduce tasks 
               may be executed in parallel.</td>
<td>true</td>
<td> </td>
<td>true</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>speculative</td>
<td>mapreduce.job.speculative.speculativecap</td>
<td>The max percent (0-1) of running tasks that
  can be speculatively re-executed at any time.</td>
<td>0.1</td>
<td> </td>
<td>0.1</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>speculative</td>
<td>mapreduce.job.speculative.slowtaskthreshold</td>
<td>
  </td>
<td>1.0</td>
<td> </td>
<td>1.0</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>speculative</td>
<td>mapreduce.job.speculative.slownodethreshold</td>
<td>The number of standard deviations by which a Task 
  Tracker's ave map and reduce progress-rates (finishTime-dispatchTime)
  must be lower than the average of all successful map/reduce task's for
  the TT to be considered too slow to give a speculative task to.
  </td>
<td>1.0</td>
<td> </td>
<td>1.0</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>job</td>
<td>mapreduce.job.jvm.numtasks</td>
<td>抛弃不适用
How many tasks to run per jvm. If set to -1, there is
  no limit. 
  </td>
<td>1</td>
<td> </td>
<td>1</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>uber</td>
<td>mapreduce.job.ubertask.enable</td>
<td>Whether to enable the small-jobs "ubertask" optimization,
  which runs "sufficiently small" jobs sequentially within a single JVM.
  "Small" is defined by the following maxmaps, maxreduces, and maxbytes
  settings.  Users may override this value.
  </td>
<td>false</td>
<td> </td>
<td>false</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>uber</td>
<td>mapreduce.job.ubertask.maxmaps</td>
<td>Threshold for number of maps, beyond which job is considered
  too big for the ubertasking optimization.  Users may override this value,
  but only downward.
  </td>
<td>9</td>
<td> </td>
<td>9</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>uber</td>
<td>mapreduce.job.ubertask.maxreduces</td>
<td>Threshold for number of reduces, beyond which job is considered
  too big for the ubertasking optimization.  CURRENTLY THE CODE CANNOT SUPPORT
  MORE THAN ONE REDUCE and will ignore larger values.  (Zero is a valid max,
  however.)  Users may override this value, but only downward.
  </td>
<td>1</td>
<td> </td>
<td>1</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>uber</td>
<td>mapreduce.job.ubertask.maxbytes</td>
<td>Threshold for number of input bytes, beyond which job is
  considered too big for the ubertasking optimization.  If no value is
  specified, dfs.block.size is used as a default.  Be sure to specify a
  default value in mapred-site.xml if the underlying filesystem is not HDFS.
  Users may override this value, but only downward.
  </td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>none</td>
<td>mapreduce.input.fileinputformat.split.minsize</td>
<td>The minimum size chunk that map input should be split
  into.  Note that some file formats may have minimum split sizes that
  take priority over this setting.</td>
<td>0</td>
<td> </td>
<td>0</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>jobtracker</td>
<td>mapreduce.jobtracker.maxtasks.perjob</td>
<td>The maximum number of tasks for a single job.
  A value of -1 indicates that there is no maximum.  </td>
<td>-1</td>
<td> </td>
<td>-1</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>job</td>
<td>mapreduce.client.submit.file.replication</td>
<td>The replication level for submitted job files.  This
  should be around the square root of the number of nodes.
  </td>
<td>10</td>
<td> </td>
<td>10</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>DNS</td>
<td>mapreduce.tasktracker.dns.interface</td>
<td>The name of the Network Interface from which a task
  tracker should report its IP address.
  </td>
<td>default</td>
<td> </td>
<td>default</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>DNS</td>
<td>mapreduce.tasktracker.dns.nameserver</td>
<td>The host name or IP address of the name server (DNS)
  which a TaskTracker should use to determine the host name used by
  the JobTracker for communication and display purposes.
  </td>
<td>default</td>
<td> </td>
<td>default</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>tasktracker</td>
<td>mapreduce.tasktracker.http.threads</td>
<td>The number of worker threads that for the http server. This is
               used for map output fetching
  </td>
<td>40</td>
<td> </td>
<td>40</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>IP端口</td>
<td>mapreduce.tasktracker.http.address</td>
<td>
    The task tracker http server address and port.
    If the port is 0 then the server will start on a free port.
  </td>
<td>0.0.0.0:50060</td>
<td> </td>
<td>0.0.0.0:50060</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>none</td>
<td>mapreduce.task.files.preserve.failedtasks</td>
<td>Should the files for failed tasks be kept. This should only be 
               used on jobs that are failing, because the storage is never
               reclaimed. It also prevents the map outputs from being erased
               from the reduce directory as they are consumed.</td>
<td>false</td>
<td> </td>
<td>false</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>压缩</td>
<td>mapreduce.output.fileoutputformat.compress</td>
<td>Should the job outputs be compressed?
  </td>
<td>false</td>
<td> </td>
<td>false</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>压缩</td>
<td>mapreduce.output.fileoutputformat.compress.type</td>
<td>If the job outputs are to compressed as SequenceFiles, how should
               they be compressed? Should be one of NONE, RECORD or BLOCK.
  </td>
<td>RECORD</td>
<td> </td>
<td>RECORD</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>压缩</td>
<td>mapreduce.output.fileoutputformat.compress.codec</td>
<td>If the job outputs are compressed, how should they be compressed?
  </td>
<td>org.apache.hadoop.io.compress.DefaultCodec</td>
<td> </td>
<td>org.apache.hadoop.io.compress.DefaultCodec</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>压缩</td>
<td>mapreduce.map.output.compress</td>
<td>Should the outputs of the maps be compressed before being
               sent across the network. Uses SequenceFile compression.
  </td>
<td>false</td>
<td> </td>
<td>false</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>压缩</td>
<td>mapreduce.map.output.compress.codec</td>
<td>If the map outputs are compressed, how should they be 
               compressed?
  </td>
<td>org.apache.hadoop.io.compress.DefaultCodec</td>
<td> </td>
<td>org.apache.hadoop.io.compress.DefaultCodec</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>job</td>
<td>map.sort.class</td>
<td>The default sort class for sorting keys.
  </td>
<td>org.apache.hadoop.util.QuickSort</td>
<td> </td>
<td>org.apache.hadoop.util.QuickSort</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>日志</td>
<td>mapreduce.task.userlog.limit.kb</td>
<td>The maximum size of user-logs of each task in KB. 0 disables the cap.
  </td>
<td>0</td>
<td> </td>
<td>0</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>日志</td>
<td>mapreduce.job.userlog.retain.hours</td>
<td>The maximum time, in hours, for which the user-logs are to be 
               retained after the job completion.
  </td>
<td>24</td>
<td> </td>
<td>24</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>jobtracker</td>
<td>mapreduce.jobtracker.hosts.filename</td>
<td>Names a file that contains the list of nodes that may
  connect to the jobtracker.  If the value is empty, all hosts are
  permitted.</td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>jobtracker</td>
<td>mapreduce.jobtracker.hosts.exclude.filename</td>
<td>Names a file that contains the list of hosts that
  should be excluded by the jobtracker.  If the value is empty, no
  hosts are excluded.</td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>jobtracker</td>
<td>mapreduce.jobtracker.heartbeats.in.second</td>
<td>Expert: Approximate number of heart-beats that could arrive 
               at JobTracker in a second. Assuming each RPC can be processed 
               in 10msec, the default value is made 100 RPCs in a second.
  </td>
<td>100</td>
<td> </td>
<td>100</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>jobtracker</td>
<td>mapreduce.jobtracker.tasktracker.maxblacklists</td>
<td>The number of blacklists for a taskTracker by various jobs
               after which the task tracker could be blacklisted across
               all jobs. The tracker will be given a tasks later
               (after a day). The tracker will become a healthy
               tracker after a restart.
  </td>
<td>4</td>
<td> </td>
<td>4</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>jobtracker</td>
<td>mapreduce.job.maxtaskfailures.per.tracker</td>
<td>The number of task-failures on a tasktracker of a given job 
               after which new tasks of that job aren't assigned to it.
  </td>
<td>3</td>
<td> </td>
<td>3</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>JobClient</td>
<td>mapreduce.client.output.filter</td>
<td>The filter for controlling the output of the task's userlogs sent
               to the console of the JobClient. 
               The permissible options are: NONE, KILLED, FAILED, SUCCEEDED and 
               ALL.
  </td>
<td>FAILED</td>
<td> </td>
<td>FAILED</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>JobClient</td>
<td>mapreduce.client.completion.pollinterval</td>
<td>The interval (in milliseconds) between which the JobClient
    polls the JobTracker for updates about job status. You may want to set this
    to a lower value to make tests run faster on a single node system. Adjusting
    this value in production may lead to unwanted client-server traffic.
    </td>
<td>5000</td>
<td> </td>
<td>5000</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>JobClient</td>
<td>mapreduce.client.progressmonitor.pollinterval</td>
<td>The interval (in milliseconds) between which the JobClient
    reports status to the console and checks for job completion. You may want to set this
    to a lower value to make tests run faster on a single node system. Adjusting
    this value in production may lead to unwanted client-server traffic.
    </td>
<td>1000</td>
<td> </td>
<td>1000</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>jobtracker</td>
<td>mapreduce.jobtracker.persist.jobstatus.active</td>
<td>Indicates if persistency of job status information is
      active or not.
    </td>
<td>true</td>
<td> </td>
<td>true</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>jobtracker</td>
<td>mapreduce.jobtracker.persist.jobstatus.hours</td>
<td>The number of hours job status information is persisted in DFS.
    The job status information will be available after it drops of the memory
    queue and between jobtracker restarts. With a zero value the job status
    information is not persisted at all in DFS.
  </td>
<td>1</td>
<td> </td>
<td>1</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>jobtracker</td>
<td>mapreduce.jobtracker.persist.jobstatus.dir</td>
<td>The directory where the job status information is persisted
      in a file system to be available after it drops of the memory queue and
      between jobtracker restarts.
    </td>
<td>/jobtracker/jobsInfo</td>
<td> </td>
<td>/jobtracker/jobsInfo</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>日志</td>
<td>mapreduce.task.profile</td>
<td>To set whether the system should collect profiler
     information for some of the tasks in this job? The information is stored
     in the user log directory. The value is "true" if task profiling
     is enabled.</td>
<td>false</td>
<td> </td>
<td>false</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>none</td>
<td>mapreduce.task.profile.maps</td>
<td> To set the ranges of map tasks to profile.
    mapreduce.task.profile has to be set to true for the value to be accounted.
    </td>
<td>0-2</td>
<td> </td>
<td>0-2</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>none</td>
<td>mapreduce.task.profile.reduces</td>
<td> To set the ranges of reduce tasks to profile.
    mapreduce.task.profile has to be set to true for the value to be accounted.
    </td>
<td>0-2</td>
<td> </td>
<td>0-2</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>skip</td>
<td>mapreduce.task.skip.start.attempts</td>
<td> The number of Task attempts AFTER which skip mode 
    will be kicked off. When skip mode is kicked off, the 
    tasks reports the range of records which it will process 
    next, to the TaskTracker. So that on failures, TT knows which 
    ones are possibly the bad records. On further executions, 
    those are skipped.
    </td>
<td>2</td>
<td> </td>
<td>2</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>skip</td>
<td>mapreduce.map.skip.proc.count.autoincr</td>
<td> The flag which if set to true, 
    SkipBadRecords.COUNTER_MAP_PROCESSED_RECORDS is incremented 
    by MapRunner after invoking the map function. This value must be set to 
    false for applications which process the records asynchronously 
    or buffer the input records. For example streaming. 
    In such cases applications should increment this counter on their own.
    </td>
<td>true</td>
<td> </td>
<td>true</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>skip</td>
<td>mapreduce.reduce.skip.proc.count.autoincr</td>
<td> The flag which if set to true, 
    SkipBadRecords.COUNTER_REDUCE_PROCESSED_GROUPS is incremented 
    by framework after invoking the reduce function. This value must be set to 
    false for applications which process the records asynchronously 
    or buffer the input records. For example streaming. 
    In such cases applications should increment this counter on their own.
    </td>
<td>true</td>
<td> </td>
<td>true</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>skip</td>
<td>mapreduce.job.skip.outdir</td>
<td> If no value is specified here, the skipped records are 
    written to the output directory at _logs/skip.
    User can stop writing skipped records by giving the value "none". 
    </td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>skip</td>
<td>mapreduce.map.skip.maxrecords</td>
<td> The number of acceptable skip records surrounding the bad 
    record PER bad record in mapper. The number includes the bad record as well.
    To turn the feature of detection/skipping of bad records off, set the 
    value to 0.
    The framework tries to narrow down the skipped range by retrying  
    until this threshold is met OR all attempts get exhausted for this task. 
    Set the value to Long.MAX_VALUE to indicate that framework need not try to 
    narrow down. Whatever records(depends on application) get skipped are 
    acceptable.
    </td>
<td>0</td>
<td> </td>
<td>0</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>skip</td>
<td>mapreduce.reduce.skip.maxgroups</td>
<td> The number of acceptable skip groups surrounding the bad 
    group PER bad group in reducer. The number includes the bad group as well.
    To turn the feature of detection/skipping of bad groups off, set the 
    value to 0.
    The framework tries to narrow down the skipped range by retrying  
    until this threshold is met OR all attempts get exhausted for this task. 
    Set the value to Long.MAX_VALUE to indicate that framework need not try to 
    narrow down. Whatever groups(depends on application) get skipped are 
    acceptable.
    </td>
<td>0</td>
<td> </td>
<td>0</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>none</td>
<td>mapreduce.ifile.readahead</td>
<td>Configuration key to enable/disable IFile readahead.
    </td>
<td>true</td>
<td> </td>
<td>true</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>none</td>
<td>mapreduce.ifile.readahead.bytes</td>
<td>Configuration key to set the IFile readahead length in bytes.
    </td>
<td>4194304</td>
<td> </td>
<td>4194304</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>end-notification</td>
<td>mapreduce.job.end-notification.retry.attempts</td>
<td>Indicates how many times hadoop should attempt to contact the
               notification URL </td>
<td>0</td>
<td> </td>
<td>0</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>end-notification</td>
<td>mapreduce.job.end-notification.retry.interval</td>
<td>Indicates time in milliseconds between notification URL retry
                calls</td>
<td>30000</td>
<td> </td>
<td>30000</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>jobtracker</td>
<td>mapreduce.jobtracker.taskcache.levels</td>
<td> This is the max level of the task cache. For example, if
    the level is 2, the tasks cached are at the host level and at the rack
    level.
  </td>
<td>2</td>
<td> </td>
<td>2</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>Scheduler</td>
<td>mapreduce.job.queuename</td>
<td> Queue to which a job is submitted. This must match one of the
    queues defined in mapred-queues.xml for the system. Also, the ACL setup
    for the queue must allow the current user to submit a job to the queue.
    Before specifying a queue, ensure that the system is configured with 
    the queue, and access is allowed for submitting jobs to the queue.
  </td>
<td>default</td>
<td> </td>
<td>default</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>Scheduler</td>
<td>mapreduce.cluster.acls.enabled</td>
<td> Specifies whether ACLs should be checked
    for authorization of users for doing various queue and job level operations.
    ACLs are disabled by default. If enabled, access control checks are made by
    JobTracker and TaskTracker when requests are made by users for queue
    operations like submit job to a queue and kill a job in the queue and job
    operations like viewing the job-details (See mapreduce.job.acl-view-job)
    or for modifying the job (See mapreduce.job.acl-modify-job) using
    Map/Reduce APIs, RPCs or via the console and web user interfaces.
    For enabling this flag(mapreduce.cluster.acls.enabled), this is to be set
    to true in mapred-site.xml on JobTracker node and on all TaskTracker nodes.
  </td>
<td>false</td>
<td> </td>
<td>false</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>Scheduler</td>
<td>mapreduce.job.acl-modify-job</td>
<td> Job specific access-control list for 'modifying' the job. It
    is only used if authorization is enabled in Map/Reduce by setting the
    configuration property mapreduce.cluster.acls.enabled to true.
    This specifies the list of users and/or groups who can do modification
    operations on the job. For specifying a list of users and groups the
    format to use is "user1,user2 group1,group". If set to '*', it allows all
    users/groups to modify this job. If set to ' '(i.e. space), it allows
    none. This configuration is used to guard all the modifications with respect
    to this job and takes care of all the following operations:
      o killing this job
      o killing a task of this job, failing a task of this job
      o setting the priority of this job
    Each of these operations are also protected by the per-queue level ACL
    "acl-administer-jobs" configured via mapred-queues.xml. So a caller should
    have the authorization to satisfy either the queue-level ACL or the
    job-level ACL.

    Irrespective of this ACL configuration, (a) job-owner, (b) the user who
    started the cluster, (c) members of an admin configured supergroup
    configured via mapreduce.cluster.permissions.supergroup and (d) queue
    administrators of the queue to which this job was submitted to configured
    via acl-administer-jobs for the specific queue in mapred-queues.xml can
    do all the modification operations on a job.

    By default, nobody else besides job-owner, the user who started the cluster,
    members of supergroup and queue administrators can perform modification
    operations on a job.
  </td>
<td> </td>
<td> </td>
<td> </td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>Scheduler</td>
<td>mapreduce.job.acl-view-job</td>
<td> Job specific access-control list for 'viewing' the job. It is
    only used if authorization is enabled in Map/Reduce by setting the
    configuration property mapreduce.cluster.acls.enabled to true.
    This specifies the list of users and/or groups who can view private details
    about the job. For specifying a list of users and groups the
    format to use is "user1,user2 group1,group". If set to '*', it allows all
    users/groups to modify this job. If set to ' '(i.e. space), it allows
    none. This configuration is used to guard some of the job-views and at
    present only protects APIs that can return possibly sensitive information
    of the job-owner like
      o job-level counters
      o task-level counters
      o tasks' diagnostic information
      o task-logs displayed on the TaskTracker web-UI and
      o job.xml showed by the JobTracker's web-UI
    Every other piece of information of jobs is still accessible by any other
    user, for e.g., JobStatus, JobProfile, list of jobs in the queue, etc.

    Irrespective of this ACL configuration, (a) job-owner, (b) the user who
    started the cluster, (c) members of an admin configured supergroup
    configured via mapreduce.cluster.permissions.supergroup and (d) queue
    administrators of the queue to which this job was submitted to configured
    via acl-administer-jobs for the specific queue in mapred-queues.xml can
    do all the view operations on a job.

    By default, nobody else besides job-owner, the user who started the
    cluster, memebers of supergroup and queue administrators can perform
    view operations on a job.
  </td>
<td> </td>
<td> </td>
<td> </td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>tasktracker</td>
<td>mapreduce.tasktracker.indexcache.mb</td>
<td> The maximum memory that a task tracker allows for the 
    index cache that is used when serving map outputs to reducers.
  </td>
<td>10</td>
<td> </td>
<td>10</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>reduce</td>
<td>mapreduce.task.merge.progress.records</td>
<td> The number of records to process during merge before
   sending a progress notification to the TaskTracker.
  </td>
<td>10000</td>
<td> </td>
<td>10000</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>reduce</td>
<td>mapreduce.job.reduce.slowstart.completedmaps</td>
<td>Fraction of the number of maps in the job which should be 
  complete before reduces are scheduled for the job. 
  </td>
<td>0.05</td>
<td> </td>
<td>0.05</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>安全</td>
<td>mapreduce.job.complete.cancel.delegation.tokens</td>
<td> if false - do not unregister/cancel delegation tokens from 
    renewal, because same tokens may be used by spawned jobs
  </td>
<td>true</td>
<td> </td>
<td>true</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>tasktracker</td>
<td>mapreduce.tasktracker.taskcontroller</td>
<td>TaskController which is used to launch and manage task execution 
  </td>
<td>org.apache.hadoop.mapred.DefaultTaskController</td>
<td> </td>
<td>org.apache.hadoop.mapred.DefaultTaskController</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>tasktracker</td>
<td>mapreduce.tasktracker.group</td>
<td>Expert: Group to which TaskTracker belongs. If 
   LinuxTaskController is configured via mapreduce.tasktracker.taskcontroller,
   the group owner of the task-controller binary should be same as this group.
  </td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>IP端口</td>
<td>mapreduce.shuffle.port</td>
<td>Default port that the ShuffleHandler will run on. ShuffleHandler 
   is a service run at the NodeManager to facilitate transfers of intermediate 
   Map outputs to requesting Reducers.
  </td>
<td>8080</td>
<td> </td>
<td>8080</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>reduce</td>
<td>mapreduce.job.reduce.shuffle.consumer.plugin.class</td>
<td>
  Name of the class whose instance will be used
  to send shuffle requests by reducetasks of this job.
  The class must be an instance of org.apache.hadoop.mapred.ShuffleConsumerPlugin.
  </td>
<td>org.apache.hadoop.mapreduce.task.reduce.Shuffle</td>
<td> </td>
<td>org.apache.hadoop.mapreduce.task.reduce.Shuffle</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>tasktracker</td>
<td>mapreduce.tasktracker.healthchecker.script.path</td>
<td>Absolute path to the script which is
  periodicallyrun by the node health monitoring service to determine if
  the node is healthy or not. If the value of this key is empty or the
  file does not exist in the location configured here, the node health
  monitoring service is not started.</td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>none</td>
<td>mapreduce.tasktracker.healthchecker.interval</td>
<td>Frequency of the node health script to be run,
  in milliseconds</td>
<td>60000</td>
<td> </td>
<td>60000</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>tasktracker</td>
<td>mapreduce.tasktracker.healthchecker.script.timeout</td>
<td>Time after node health script should be killed if 
  unresponsive and considered that the script has failed.</td>
<td>600000</td>
<td> </td>
<td>600000</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>tasktracker</td>
<td>mapreduce.tasktracker.healthchecker.script.args</td>
<td>List of arguments which are to be passed to 
  node health script when it is being launched comma seperated.
  </td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>none</td>
<td>mapreduce.job.counters.limit</td>
<td>Limit on the number of user counters allowed per job.
  </td>
<td>120</td>
<td> </td>
<td>120</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>YARN</td>
<td>mapreduce.framework.name</td>
<td>The runtime framework for executing MapReduce jobs.
  Can be one of local, classic or yarn.
  </td>
<td>local</td>
<td> </td>
<td>local</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>hdfs目录</td>
<td>yarn.app.mapreduce.am.staging-dir</td>
<td>The staging dir used while submitting jobs.
  </td>
<td>/tmp/hadoop-yarn/staging</td>
<td> </td>
<td>/user</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>end-notification</td>
<td>mapreduce.job.end-notification.max.attempts</td>
<td>The maximum number of times a URL will be read for providing job
    end notification. Cluster administrators can set this to limit how long
    after end of a job, the Application Master waits before exiting. Must be
    marked as final to prevent users from overriding this.
  </td>
<td>5</td>
<td>final</td>
<td>5</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>end-notification</td>
<td>mapreduce.job.end-notification.max.retry.interval</td>
<td>The maximum amount of time (in seconds) to wait before retrying
    job end notification. Cluster administrators can set this to limit how long
    the Application Master waits before exiting. Must be marked as final to
    prevent users from overriding this.</td>
<td>5</td>
<td>final</td>
<td>5</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>end-notification</td>
<td>mapreduce.job.end-notification.url</td>
<td>The URL to send job end notification. It may contain sentinels
    $jobId and $jobStatus which will be replaced with jobId and jobStatus.
  </td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>end-notification</td>
<td>mapreduce.job.end-notification.retry.attempts</td>
<td>The number of times the submitter of the job wants to retry job
    end notification if it fails. This is capped by
    mapreduce.job.end-notification.max.attempts</td>
<td>5</td>
<td> </td>
<td>5</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>end-notification</td>
<td>mapreduce.job.end-notification.retry.interval</td>
<td>The number of seconds the submitter of the job wants to wait
    before job end notification is retried if it fails. This is capped by
    mapreduce.job.end-notification.max.retry.interval</td>
<td>1</td>
<td> </td>
<td>1</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>MRAM</td>
<td>yarn.app.mapreduce.am.env</td>
<td>User added environment variables for the MR App Master 
  processes. Example :
  1) A=foo  This will set the env variable A to foo
  2) B=$B:c This is inherit tasktracker's B env variable.  
  </td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>MRAM</td>
<td>yarn.app.mapreduce.am.command-opts</td>
<td>Java opts for the MR App Master processes.  
  The following symbol, if present, will be interpolated: @taskid@ is replaced 
  by current TaskID. Any other occurrences of '@' will go unchanged.
  For example, to enable verbose gc logging to a file named for the taskid in
  /tmp and to set the heap maximum to be a gigabyte, pass a 'value' of:
        -Xmx1024m -verbose:gc -Xloggc:/tmp/@taskid@.gc
  
  Usage of -Djava.library.path can cause programs to no longer function if
  hadoop native libraries are used. These values should instead be set as part 
  of LD_LIBRARY_PATH in the map / reduce JVM env using the mapreduce.map.env and 
  mapreduce.reduce.env config settings. 
  跟AM申请内存挂钩
  </td>
<td>-Xmx1024m</td>
<td> </td>
<td>-Xmx1024m</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>MRAM</td>
<td>yarn.app.mapreduce.am.job.task.listener.thread-count</td>
<td>The number of threads used to handle RPC calls in the 
    MR AppMaster from remote tasks</td>
<td>30</td>
<td> </td>
<td>30</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>MRAM</td>
<td>yarn.app.mapreduce.am.job.client.port-range</td>
<td>Range of ports that the MapReduce AM can use when binding.
    Leave blank if you want all possible ports.  
    For example 50000-50050,50100-50200</td>
<td>null</td>
<td> </td>
<td>null</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>MRAM</td>
<td>yarn.app.mapreduce.am.job.committer.cancel-timeout</td>
<td>The amount of time in milliseconds to wait for the output
    committer to cancel an operation if the job is killed</td>
<td>60000</td>
<td> </td>
<td>60000</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>MRAM</td>
<td>yarn.app.mapreduce.am.scheduler.heartbeat.interval-ms</td>
<td>The interval in ms at which the MR AppMaster should send
    heartbeats to the ResourceManager</td>
<td>1000</td>
<td> </td>
<td>1000</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>MRAM</td>
<td>yarn.app.mapreduce.client-am.ipc.max-retries</td>
<td>The number of client retries to the AM - before reconnecting
    to the RM to fetch Application Status.</td>
<td>3</td>
<td> </td>
<td>3</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>MRAM</td>
<td>yarn.app.mapreduce.client.max-retries</td>
<td>The number of client retries to the RM/HS/AM before
    throwing exception. This is a layer above the ipc.</td>
<td>3</td>
<td> </td>
<td>3</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>MRAM</td>
<td>yarn.app.mapreduce.am.resource.mb</td>
<td>The amount of memory the MR AppMaster needs.AM申请的内存</td>
<td>1536</td>
<td> </td>
<td>1536</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>MRAM</td>
<td>mapreduce.application.classpath</td>
<td>CLASSPATH for MR applications. A comma-separated list
  of CLASSPATH entries</td>
<td>$HADOOP_MAPRED_HOME/share/hadoop/mapreduce/*,$HADOOP_MAPRED_HOME/share/hadoop/mapreduce/lib/*</td>
<td> </td>
<td>$HADOOP_MAPRED_HOME/share/hadoop/mapreduce/*,$HADOOP_MAPRED_HOME/share/hadoop/mapreduce/lib/*</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>IP端口</td>
<td>mapreduce.jobhistory.address</td>
<td>MapReduce JobHistory Server IPC host:port</td>
<td>0.0.0.0:10020</td>
<td> </td>
<td>0.0.0.0:10020</td>
<td>I9</td>
</tr>

<tr>
<td>cdh4.3.0</td>
<td>JHAdminConfig</td>
<td>IP端口</td>
<td>mapreduce.jobhistory.cleaner.enable</td>
<td>是否开启jobhistory的自动清理</td>
<td>false</td>
<td> </td>
<td>false</td>
<td>I5</td>
</tr>

<tr>
<td>cdh4.3.0</td>
<td>JHAdminConfig</td>
<td>IP端口</td>
<td>mapreduce.jobhistory.cleaner.interval-ms</td>
<td>jobhistory的自动清理间隔</td>
<td>1 * 24 * 60 * 60 * 1000 1day</td>
<td> </td>
<td>1 * 24 * 60 * 60 * 1000 1day</td>
<td>I5</td>
</tr>

<tr>
<td>cdh4.3.0</td>
<td>JHAdminConfig</td>
<td>IP端口</td>
<td>mapreduce.jobhistory.client.thread-count</td>
<td>jobhistory的客户端线程</td>
<td>10</td>
<td> </td>
<td>10</td>
<td>I5</td>
</tr>

<tr>
<td>cdh4.3.0</td>
<td>JHAdminConfig</td>
<td>IP端口</td>
<td>mapreduce.jobhistory.datestring.cache.size</td>
<td>jobhistory的缓存的字符串总量大小，会影响扫描是jobid的数量上限</td>
<td>200000</td>
<td> </td>
<td>200000</td>
<td>I5</td>
</tr>

<tr>
<td>cdh4.3.0</td>
<td>JHAdminConfig</td>
<td>IP端口</td>
<td>mapreduce.jobhistory.done-dir</td>
<td>jobhistory的完成目录,会自动添加/history/done</td>
<td>${yarn.app.mapreduce.am.staging-dir}</td>
<td> </td>
<td>/jobhistory</td>
<td>I5</td>
</tr>

<tr>
<td>cdh4.3.0</td>
<td>JHAdminConfig</td>
<td>IP端口</td>
<td>mapreduce.jobhistory.intermediate-done-dir</td>
<td>jobhistory的中间目录,会自动添加/history/done_intermediate</td>
<td>${yarn.app.mapreduce.am.staging-dir}</td>
<td> </td>
<td>/jobhistory</td>
<td>I5</td>
</tr>

<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>IP端口</td>
<td>mapreduce.jobhistory.webapp.address</td>
<td>MapReduce JobHistory Server Web UI host:port</td>
<td>0.0.0.0:19888</td>
<td> </td>
<td>0.0.0.0:19888</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>安全</td>
<td>mapreduce.jobhistory.keytab</td>
<td>
    Location of the kerberos keytab file for the MapReduce
    JobHistory Server.
  </td>
<td>/etc/security/keytab/jhs.service.keytab</td>
<td> </td>
<td>/etc/security/keytab/jhs.service.keytab</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>安全</td>
<td>mapreduce.jobhistory.principal</td>
<td>
    Kerberos principal name for the MapReduce JobHistory Server.
  </td>
<td>jhs/_HOST@REALM.TLD</td>
<td> </td>
<td>jhs/_HOST@REALM.TLD</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>mapred-default.xml</td>
<td>job</td>
<td>mapreduce.job.map.output.collector.class</td>
<td>
    It defines the MapOutputCollector implementation to use.
  </td>
<td>org.apache.hadoop.mapred.MapTask$MapOutputBuffer</td>
<td> </td>
<td>org.apache.hadoop.mapred.MapTask$MapOutputBuffer</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>distcp-default.xml</td>
<td>distcp</td>
<td>distcp.dynamic.strategy.impl</td>
<td>Implementation of dynamic input format</td>
<td>org.apache.hadoop.tools.mapred.lib.DynamicInputFormat</td>
<td> </td>
<td>org.apache.hadoop.tools.mapred.lib.DynamicInputFormat</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>distcp-default.xml</td>
<td>distcp</td>
<td>distcp.static.strategy.impl</td>
<td>Implementation of static input format</td>
<td>org.apache.hadoop.tools.mapred.UniformSizeInputFormat</td>
<td> </td>
<td>org.apache.hadoop.tools.mapred.UniformSizeInputFormat</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>distcp-default.xml</td>
<td>distcp</td>
<td>mapred.job.map.memory.mb</td>
<td>null</td>
<td>1024</td>
<td> </td>
<td>1024</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>distcp-default.xml</td>
<td>distcp</td>
<td>mapred.job.reduce.memory.mb</td>
<td>null</td>
<td>1024</td>
<td> </td>
<td>1024</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>distcp-default.xml</td>
<td>distcp</td>
<td>mapred.reducer.new-api</td>
<td>null</td>
<td>true</td>
<td> </td>
<td>true</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>distcp-default.xml</td>
<td>distcp</td>
<td>mapreduce.reduce.class</td>
<td>null</td>
<td>org.apache.hadoop.mapreduce.Reducer</td>
<td> </td>
<td>org.apache.hadoop.mapreduce.Reducer</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>YARN</td>
<td>yarn.ipc.client.factory.class</td>
<td>Factory to create client IPC classes.</td>
<td>null</td>
<td> </td>
<td>null</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>YARN</td>
<td>yarn.ipc.serializer.type</td>
<td>Type of serialization to use.</td>
<td>protocolbuffers</td>
<td> </td>
<td>protocolbuffers</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>YARN</td>
<td>yarn.ipc.server.factory.class</td>
<td>Factory to create server IPC classes.</td>
<td>null</td>
<td> </td>
<td>null</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>YARN</td>
<td>yarn.ipc.exception.factory.class</td>
<td>Factory to create IPC exceptions.</td>
<td>null</td>
<td> </td>
<td>null</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>YARN</td>
<td>yarn.ipc.record.factory.class</td>
<td>Factory to create serializeable records.</td>
<td>null</td>
<td> </td>
<td>null</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>YARN</td>
<td>yarn.ipc.rpc.class</td>
<td>RPC class implementation</td>
<td>org.apache.hadoop.yarn.ipc.HadoopYarnProtoRPC</td>
<td> </td>
<td>org.apache.hadoop.yarn.ipc.HadoopYarnProtoRPC</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>IP端口</td>
<td>yarn.resourcemanager.address</td>
<td>The address of the applications manager interface in the RM.</td>
<td>0.0.0.0:8032</td>
<td> </td>
<td>0.0.0.0:8032</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>RM</td>
<td>yarn.resourcemanager.client.thread-count</td>
<td>The number of threads used to handle applications manager requests.</td>
<td>50</td>
<td> </td>
<td>50</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>MRAM</td>
<td>yarn.am.liveness-monitor.expiry-interval-ms</td>
<td>The expiry interval for application master reporting.</td>
<td>600000</td>
<td> </td>
<td>600000</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>安全</td>
<td>yarn.resourcemanager.principal</td>
<td>The Kerberos principal for the resource manager.</td>
<td>null</td>
<td> </td>
<td>null</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>IP端口</td>
<td>yarn.resourcemanager.scheduler.address</td>
<td>The address of the scheduler interface.</td>
<td>0.0.0.0:8030</td>
<td> </td>
<td>0.0.0.0:8030</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>RM</td>
<td>yarn.resourcemanager.scheduler.client.thread-count</td>
<td>Number of threads to handle scheduler interface.</td>
<td>50</td>
<td> </td>
<td>50</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>IP端口</td>
<td>yarn.resourcemanager.webapp.address</td>
<td>The address of the RM web application.</td>
<td>0.0.0.0:8088</td>
<td> </td>
<td>0.0.0.0:8088</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>IP端口</td>
<td>yarn.resourcemanager.resource-tracker.address</td>
<td>null</td>
<td>0.0.0.0:8031</td>
<td> </td>
<td>0.0.0.0:8031</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>安全</td>
<td>yarn.acl.enable</td>
<td>Are acls enabled.</td>
<td>true</td>
<td> </td>
<td>true</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>安全</td>
<td>yarn.admin.acl</td>
<td>ACL of who can be admin of the YARN cluster.</td>
<td>*</td>
<td> </td>
<td>*</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>IP端口</td>
<td>yarn.resourcemanager.admin.address</td>
<td>The address of the RM admin interface.</td>
<td>0.0.0.0:8033</td>
<td> </td>
<td>0.0.0.0:8033</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>RM</td>
<td>yarn.resourcemanager.admin.client.thread-count</td>
<td>Number of threads used to handle RM admin interface.</td>
<td>1</td>
<td> </td>
<td>1</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>RM</td>
<td>yarn.resourcemanager.amliveliness-monitor.interval-ms</td>
<td>How often should the RM check that the AM is still alive.</td>
<td>1000</td>
<td> </td>
<td>1000</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>MRAM</td>
<td>yarn.resourcemanager.am.max-retries</td>
<td>The maximum number of application master retries.服务端参数。重启生效。</td>
<td>1</td>
<td> </td>
<td>3</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>RM</td>
<td>yarn.resourcemanager.container.liveness-monitor.interval-ms</td>
<td>How often to check that containers are still alive. </td>
<td>600000</td>
<td> </td>
<td>600000</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>安全</td>
<td>yarn.resourcemanager.keytab</td>
<td>The keytab for the resource manager.</td>
<td>/etc/krb5.keytab</td>
<td> </td>
<td>/etc/krb5.keytab</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>NM</td>
<td>yarn.nm.liveness-monitor.expiry-interval-ms</td>
<td>How long to wait until a node manager is considered dead.</td>
<td>600000</td>
<td> </td>
<td>600000</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>NM</td>
<td>yarn.resourcemanager.nm.liveness-monitor.interval-ms</td>
<td>How often to check that node managers are still alive.</td>
<td>1000</td>
<td> </td>
<td>1000</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>YARN</td>
<td>yarn.resourcemanager.nodes.include-path</td>
<td>Path to file with nodes to include.</td>
<td>null</td>
<td> </td>
<td>null</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>YARN</td>
<td>yarn.resourcemanager.nodes.exclude-path</td>
<td>Path to file with nodes to exclude.</td>
<td>null</td>
<td> </td>
<td>null</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>RM</td>
<td>yarn.resourcemanager.resource-tracker.client.thread-count</td>
<td>Number of threads to handle resource tracker calls.</td>
<td>50</td>
<td> </td>
<td>50</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>scheduler</td>
<td>yarn.resourcemanager.scheduler.class</td>
<td>The class to use as the resource scheduler.</td>
<td>org.apache.hadoop.yarn.server.resourcemanager.scheduler.fifo.FifoScheduler</td>
<td> </td>
<td>org.apache.hadoop.yarn.server.resourcemanager.scheduler.fifo.FifoScheduler</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>scheduler</td>
<td>yarn.scheduler.minimum-allocation-mb</td>
<td>The minimum allocation size for every container request at the RM,
    in MBs. Memory requests lower than this won't take effect,
    and the specified value will get allocated at minimum.</td>
<td>1024</td>
<td> </td>
<td>1024</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>scheduler</td>
<td>yarn.scheduler.maximum-allocation-mb</td>
<td>The maximum allocation size for every container request at the RM,
    in MBs. Memory requests higher than this won't take effect,
    and will get capped to this value.</td>
<td>8192</td>
<td> </td>
<td>8192</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>RM</td>
<td>yarn.resourcemanager.recovery.enabled</td>
<td>Enable RM to recover state after starting. If true, then 
    yarn.resourcemanager.store.class must be specified
	RM状态保存特性
	</td>
<td>false</td>
<td> </td>
<td>false</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>none</td>
<td>yarn.resourcemanager.store.class</td>
<td>The class to use as the persistent store.
RM状态保存的类
</td>
<td>null</td>
<td> </td>
<td>null</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>RM</td>
<td>yarn.resourcemanager.max-completed-applications</td>
<td>The maximum number of completed applications RM keeps.保存的app的个数 </td>
<td>10000</td>
<td> </td>
<td>10000</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>RM</td>
<td>yarn.resourcemanager.delayed.delegation-token.removal-interval-ms</td>
<td>Interval at which the delayed token removal thread runs</td>
<td>30000</td>
<td> </td>
<td>30000</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>RM</td>
<td>yarn.resourcemanager.application-tokens.master-key-rolling-interval-secs</td>
<td>Interval for the roll over for the master key used to generate
        application tokens
    </td>
<td>86400</td>
<td> </td>
<td>86400</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>RM</td>
<td>yarn.resourcemanager.container-tokens.master-key-rolling-interval-secs</td>
<td>Interval for the roll over for the master key used to generate
        container tokens. It is expected to be much greater than
        yarn.nm.liveness-monitor.expiry-interval-ms and
        yarn.rm.container-allocation.expiry-interval-ms. Otherwise the
        behavior is undefined.
    </td>
<td>86400</td>
<td> </td>
<td>86400</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>IP端口</td>
<td>yarn.nodemanager.address</td>
<td>The address of the container manager in the NM.</td>
<td>0.0.0.0:0</td>
<td> </td>
<td>0.0.0.0:0</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>NM</td>
<td>yarn.nodemanager.admin-env</td>
<td>Environment variables that should be forwarded from the NodeManager's environment to the container's.环境变量继承</td>
<td>MALLOC_ARENA_MAX=$MALLOC_ARENA_MAX</td>
<td> </td>
<td>MALLOC_ARENA_MAX=$MALLOC_ARENA_MAX</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>NM</td>
<td>yarn.nodemanager.env-whitelist</td>
<td>Environment variables that containers may override rather than use NodeManager's default.
允许container自己配置的环境变量
</td>
<td>JAVA_HOME,HADOOP_COMMON_HOME,HADOOP_HDFS_HOME,HADOOP_CONF_DIR,YARN_HOME</td>
<td> </td>
<td>JAVA_HOME,HADOOP_COMMON_HOME,HADOOP_HDFS_HOME,HADOOP_CONF_DIR,YARN_HOME</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>NM</td>
<td>yarn.nodemanager.container-executor.class</td>
<td>who will execute(launch) the containers.container运行类</td>
<td>org.apache.hadoop.yarn.server.nodemanager.DefaultContainerExecutor</td>
<td> </td>
<td>org.apache.hadoop.yarn.server.nodemanager.DefaultContainerExecutor</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>NM</td>
<td>yarn.nodemanager.container-manager.thread-count</td>
<td>Number of threads container manager uses.</td>
<td>20</td>
<td> </td>
<td>20</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>NM</td>
<td>yarn.nodemanager.delete.thread-count</td>
<td>Number of threads used in cleanup.</td>
<td>4</td>
<td> </td>
<td>4</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>NM</td>
<td>yarn.nodemanager.delete.debug-delay-sec</td>
<td>
      Number of seconds after an application finishes before the nodemanager's 
      DeletionService will delete the application's localized file directory
      and log directory.
      
      To diagnose Yarn application problems, set this property's value large
      enough (for example, to 600 = 10 minutes) to permit examination of these
      directories. After changing the property's value, you must restart the 
      nodemanager in order for it to have an effect.

      The roots of Yarn applications' work directories is configurable with
      the yarn.nodemanager.local-dirs property (see below), and the roots
      of the Yarn applications' log directories is configurable with the 
      yarn.nodemanager.log-dirs property (see also below).
	  用于debug模式下NM延迟删除日志
    </td>
<td>0</td>
<td> </td>
<td>0</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>NM</td>
<td>yarn.nodemanager.heartbeat.interval-ms</td>
<td>Heartbeat interval to RM</td>
<td>1000</td>
<td> </td>
<td>1000</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>安全</td>
<td>yarn.nodemanager.keytab</td>
<td>Keytab for NM.</td>
<td>/etc/krb5.keytab</td>
<td> </td>
<td>/etc/krb5.keytab</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>本地目录</td>
<td>yarn.nodemanager.local-dirs</td>
<td>List of directories to store localized files in. An 
      application's localized file directory will be found in:
      ${yarn.nodemanager.local-dirs}/usercache/${user}/appcache/application_${appid}.
      Individual containers' work directories, called container_${contid}, will
      be subdirectories of this.
   </td>
<td>${hadoop.tmp.dir}/nm-local-dir</td>
<td> </td>
<td>/home/hadoop/yarn_nm/nm-local-dir</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>IP端口</td>
<td>yarn.nodemanager.localizer.address</td>
<td>Address where the localizer IPC is.</td>
<td>0.0.0.0:8040</td>
<td> </td>
<td>0.0.0.0:8040</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>NM</td>
<td>yarn.nodemanager.localizer.cache.cleanup.interval-ms</td>
<td>Interval in between cache cleanups.</td>
<td>600000</td>
<td> </td>
<td>600000</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>NM</td>
<td>yarn.nodemanager.localizer.cache.target-size-mb</td>
<td>Target size of localizer cache in MB, per local directory.</td>
<td>10240</td>
<td> </td>
<td>10240</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>NM</td>
<td>yarn.nodemanager.localizer.client.thread-count</td>
<td>Number of threads to handle localization requests.</td>
<td>5</td>
<td> </td>
<td>5</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>NM</td>
<td>yarn.nodemanager.localizer.fetch.thread-count</td>
<td>Number of threads to use for localization fetching.</td>
<td>4</td>
<td> </td>
<td>4</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>本地目录</td>
<td>yarn.nodemanager.log-dirs</td>
<td>
      Where to store container logs. An application's localized log directory 
      will be found in ${yarn.nodemanager.log-dirs}/application_${appid}.
      Individual containers' log directories will be below this, in directories 
      named container_{$contid}. Each container directory will contain the files
      stderr, stdin, and syslog generated by that container.
    </td>
<td>${yarn.log.dir}/userlogs</td>
<td> </td>
<td>/home/hadoop/yarn_nm/nuserlogs</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>日志</td>
<td>yarn.log-aggregation-enable</td>
<td>Whether to enable log aggregation 日志会从各个AM汇总到hdfs</td>
<td>false</td>
<td> </td>
<td>true</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>日志</td>
<td>yarn.log-aggregation.retain-seconds </td>
<td>How long to keep aggregation logs before deleting them.  -1 disables. 
    Be careful set this too small and you will spam the name node.
	jobhistory中可以设置多长时间删除job的运行日志，
	默认不删除，如果设置值太少会导致nn有问题？</td>
<td>-1</td>
<td> </td>
<td>-1</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>NM</td>
<td>yarn.nodemanager.log.retain-seconds</td>
<td>Time in seconds to retain user logs. Only applicable if
    log aggregation is disabled
	nm上保留用户日志的时间
    </td>
<td>10800</td>
<td> </td>
<td>10800</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>HDFS目录</td>
<td>yarn.nodemanager.remote-app-log-dir</td>
<td>Where to aggregate logs to.</td>
<td>/tmp/logs</td>
<td> </td>
<td>/user</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>HDFS目录</td>
<td>yarn.nodemanager.remote-app-log-dir-suffix</td>
<td>The remote log dir will be created at 
      {yarn.nodemanager.remote-app-log-dir}/${user}/{thisParam}
    </td>
<td>logs</td>
<td> </td>
<td>logs</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>NM</td>
<td>yarn.nodemanager.resource.memory-mb</td>
<td>Amount of physical memory, in MB, that can be allocated 
    for containers.</td>
<td>8192</td>
<td> </td>
<td>8192</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>NM</td>
<td>yarn.nodemanager.vmem-pmem-ratio</td>
<td>Ratio between virtual memory to physical memory when
    setting memory limits for containers. Container allocations are
    expressed in terms of physical memory, and virtual memory usage
    is allowed to exceed this allocation by this ratio.
	虚拟地址的是物理地址的倍数上限
    </td>
<td>2.1</td>
<td> </td>
<td>4.1</td>
<td>I9</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>IP端口</td>
<td>yarn.nodemanager.webapp.address</td>
<td>NM Webapp address.</td>
<td>0.0.0.0:8042</td>
<td> </td>
<td>0.0.0.0:8042</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>NM</td>
<td>yarn.nodemanager.container-monitor.interval-ms</td>
<td>How often to monitor containers.</td>
<td>3000</td>
<td> </td>
<td>3000</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>NM</td>
<td>yarn.nodemanager.container-monitor.resource-calculator.class</td>
<td>Class that calculates containers current resource utilization.</td>
<td>null</td>
<td> </td>
<td>null</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>NM</td>
<td>yarn.nodemanager.health-checker.interval-ms</td>
<td>Frequency of running node health script.</td>
<td>600000</td>
<td> </td>
<td>600000</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>NM</td>
<td>yarn.nodemanager.health-checker.script.timeout-ms</td>
<td>Script time out period.</td>
<td>1200000</td>
<td> </td>
<td>1200000</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>NM</td>
<td>yarn.nodemanager.health-checker.script.path</td>
<td>The health check script to run.</td>
<td>null</td>
<td> </td>
<td>null</td>
<td>I5</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>NM</td>
<td>yarn.nodemanager.health-checker.script.opts</td>
<td>The arguments to pass to the health check script.</td>
<td>null</td>
<td> </td>
<td>null</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>NM</td>
<td>yarn.nodemanager.disk-health-checker.interval-ms</td>
<td>Frequency of running disk health checker code.</td>
<td>120000</td>
<td> </td>
<td>120000</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>NM</td>
<td>yarn.nodemanager.disk-health-checker.min-healthy-disks</td>
<td>The minimum fraction of number of disks to be healthy for the
    nodemanager to launch new containers. This correspond to both
    yarn-nodemanager.local-dirs and yarn.nodemanager.log-dirs. i.e. If there
    are less number of healthy local-dirs (or log-dirs) available, then
    new containers will not be launched on this node.</td>
<td>0.25</td>
<td> </td>
<td>0.25</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>linux-container</td>
<td>yarn.nodemanager.linux-container-executor.path</td>
<td>The path to the Linux container executor.</td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>压缩</td>
<td>yarn.nodemanager.log-aggregation.compression-type</td>
<td>T-file compression types used to compress aggregated logs.</td>
<td>none</td>
<td> </td>
<td>none</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>安全</td>
<td>yarn.nodemanager.principal</td>
<td>The kerberos principal for the node manager.</td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>安全</td>
<td>yarn.nodemanager.aux-services</td>
<td>null</td>
<td>null</td>
<td> </td>
<td>null</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>NM</td>
<td>yarn.nodemanager.sleep-delay-before-sigkill.ms</td>
<td>No. of ms to wait between sending a SIGTERM and SIGKILL to a container</td>
<td>250</td>
<td> </td>
<td>250</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>NM</td>
<td>yarn.nodemanager.process-kill-wait.ms</td>
<td>Max time to wait for a process to come up when trying to cleanup a container</td>
<td>2000</td>
<td> </td>
<td>2000</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>安全</td>
<td>yarn.nodemanager.aux-services.mapreduce.shuffle.class</td>
<td>null</td>
<td>org.apache.hadoop.mapred.ShuffleHandler</td>
<td> </td>
<td>org.apache.hadoop.mapred.ShuffleHandler</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>job</td>
<td>mapreduce.job.jar</td>
<td>null</td>
<td>null</td>
<td> </td>
<td>null</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>none</td>
<td>mapreduce.job.hdfs-servers</td>
<td>job</td>
<td>${fs.defaultFS}</td>
<td> </td>
<td>${fs.defaultFS}</td>
<td>I1</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>安全</td>
<td>yarn.web-proxy.principal</td>
<td>The kerberos principal for the proxy, if the proxy is not
    running as part of the RM.</td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>安全</td>
<td>yarn.web-proxy.keytab</td>
<td>Keytab for WebAppProxy, if the proxy is not running as part of 
    the RM.</td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>RM</td>
<td>yarn.web-proxy.address</td>
<td>The address for the web proxy as HOST:PORT, if this is not
     given then the proxy will run as part of the RM</td>
<td>null</td>
<td> </td>
<td>null</td>
<td>0</td>
</tr>
<tr>
<td>cdh4.3.0</td>
<td>yarn-default.xml</td>
<td>RMAM</td>
<td>yarn.application.classpath</td>
<td>CLASSPATH for YARN applications. A comma-separated list
    of CLASSPATH entries</td>
<td>$HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/share/hadoop/common/*,$HADOOP_COMMON_HOME/share/hadoop/common/lib/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/lib/*,$YARN_HOME/share/hadoop/yarn/*,$YARN_HOME/share/hadoop/yarn/lib/*</td>
<td> </td>
<td>$HADOOP_CONF_DIR,$HADOOP_COMMON_HOME/share/hadoop/common/*,$HADOOP_COMMON_HOME/share/hadoop/common/lib/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/*,$HADOOP_HDFS_HOME/share/hadoop/hdfs/lib/*,$YARN_HOME/share/hadoop/yarn/*,$YARN_HOME/share/hadoop/yarn/lib/*</td>
<td>0</td>
</tr>
</tbody>
</table>

<script type="text/javascript" >
$(document).ready(function() {
    $('#hadooptable').dataTable();
} );
</script>