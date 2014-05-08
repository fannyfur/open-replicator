open-replicator
===============

Open Replicator is a high performance MySQL binlog parser written in Java. It unfolds the possibilities that you can parse, filter and broadcast the binlog events in a real time manner.

note

For MySQL 5.6.6 users, binlog_checksum system variable is NOT supported by open-replicator at the moment, please set it to NONE.

releases

1.0.6

    release date: 2014-05-08
    remove dependency commons-lang, log4j
    support MYSQL_TYPE_TIMESTAMP2, MYSQL_TYPE_DATETIME2, MYSQL_TYPE_TIME2 

maven

<dependency>
        <groupId>open-replicator</groupId>
        <artifactId>open-replicator</artifactId>
        <version>1.0.6</version>
</dependency>

usage

final OpenReplicator or = new OpenReplicator();
or.setUser("root");
or.setPassword("123456");
or.setHost("localhost");
or.setPort(3306);
or.setServerId(6789);
or.setBinlogPosition(4);
or.setBinlogFileName("mysql_bin.000001");
or.setBinlogEventListener(new BinlogEventListener() {
    public void onEvents(BinlogEventV4 event) {
        // your code goes here
    }
});
or.start();

System.out.println("press 'q' to stop");
final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
for(String line = br.readLine(); line != null; line = br.readLine()) {
    if(line.equals("q")) {
        or.stop();
        break;
    }
}
