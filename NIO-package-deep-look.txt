#### IO vs NIO
| IO  | NIO |
|--|--|
|Stream based API|Buffered AIP|
|Block IO call|Non-blocking IO call|
||Selectors|

### NIO Use cases
####  Change notification
NIO.2 gives us a better way to express change detection
``` 
	import java.nio.file.attribute.*;
    import java.io.*;
    import java.util.*;
    import java.nio.file.Path;
    import java.nio.file.Paths;
    import java.nio.file.StandardWatchEventKinds;
    import java.nio.file.WatchEvent;
    import java.nio.file.WatchKey;
    import java.nio.file.WatchService;
    import java.util.List;
    
    public class Watcher {
        public static void main(String[] args) {
            Path this_dir = Paths.get(".");    
            System.out.println("Now watching the current directory ..."); 
            try {
                WatchService watcher = this_dir.getFileSystem().newWatchService();
                this_dir.register(watcher, StandardWatchEventKinds.ENTRY_CREATE);
     
                WatchKey watckKey = watcher.take();
     
                List<WatchEvent< &64;>> events = watckKey.pollEvents();
                for (WatchEvent event : events) {
                    System.out.println("Someone just created the file '" + event.context().toString() + "'.");
               }
           } catch (Exception e) {
               System.out.println("Error: " + e.toString());
           }
        }
    }
```

#### Selectors and asynchronous I/O: Selectors help multiplex
demonstrates the use of NIO selectors in a multi-port networking echo-er, a program slightly modified from one created by Greg Travis in 2003 (see [Resources](http://www.javaworld.com/#resources)). Unix and Unix-like operating systems have long had efficient implementations of selectors, so this sort of networking program is a model of good performance for a Java-coded networking program.

    import java.io.*;
    import java.net.*;
    import java.nio.*;
    import java.nio.channels.*;
    import java.util.*;
    
    public class MultiPortEcho
    {
      private int ports[];
      private ByteBuffer echoBuffer = ByteBuffer.allocate( 1024 );
    
      public MultiPortEcho( int ports[] ) throws IOException {
        this.ports = ports;
    
        configure_selector();
      }
    
      private void configure_selector() throws IOException {
        // Create a new selector
        Selector selector = Selector.open();
    
        // Open a listener on each port, and register each one
        // with the selector
        for (int i=0; i<ports.length; ++i) {
          ServerSocketChannel ssc = ServerSocketChannel.open();
          ssc.configureBlocking(false);
          ServerSocket ss = ssc.socket();
          InetSocketAddress address = new InetSocketAddress(ports[i]);
          ss.bind(address);
    
          SelectionKey key = ssc.register(selector, SelectionKey.OP_ACCEPT);
    
          System.out.println("Going to listen on " + ports[i]);
        }
    
        while (true) {
          int num = selector.select();
    
          Set selectedKeys = selector.selectedKeys();
          Iterator it = selectedKeys.iterator();
    
          while (it.hasNext()) {
            SelectionKey key = (SelectionKey) it.next();
    
            if ((key.readyOps() & SelectionKey.OP_ACCEPT)
              == SelectionKey.OP_ACCEPT) {
              // Accept the new connection
              ServerSocketChannel ssc = (ServerSocketChannel)key.channel();
              SocketChannel sc = ssc.accept();
              sc.configureBlocking(false);
    
              // Add the new connection to the selector
              SelectionKey newKey = sc.register(selector, SelectionKey.OP_READ);
              it.remove();
    
              System.out.println( "Got connection from "+sc );
            } else if ((key.readyOps() & SelectionKey.OP_READ)
              == SelectionKey.OP_READ) {
              // Read the data
              SocketChannel sc = (SocketChannel)key.channel();
    
              // Echo data
              int bytesEchoed = 0;
              while (true) {
                echoBuffer.clear();
    
                int number_of_bytes = sc.read(echoBuffer);
    
                if (number_of_bytes <= 0) {
                  break;
                }
    
                echoBuffer.flip();
    
                sc.write(echoBuffer);
                bytesEchoed += number_of_bytes;
              }
    
              System.out.println("Echoed " + bytesEchoed + " from " + sc);
    
              it.remove();
            }
    
          }
        }
      }
    
      static public void main( String args[] ) throws Exception {
        if (args.length<=0) {
          System.err.println("Usage: java MultiPortEcho port [port port ...]");
          System.exit(1);
        }
    
        int ports[] = new int[args.length];
    
        for (int i=0; i<args.length; ++i) {
          ports[i] = Integer.parseInt(args[i]);
        }
    
        new MultiPortEcho(ports);
      }
    }

#### Memory mapping
_Memory mapping_ is an OS-level service that makes segments of a file appear for programming purposes like areas of memory.
Memory mapping has a number of consequences and implications, more than I'll get into here. At a high level, it helps make I/O happen at the speed of memory access, rather than file access.

    import java.io.RandomAccessFile;
	import java.nio.MappedByteBuffer;
	import java.nio.channels.FileChannel;

	  public class mem_map_example {
		  private static int mem_map_size = 20 * 1024 * 1024;
		  private static String fn = "example_memory_mapped_file.txt";

		  public static void main(String[] args) throws Exception {
			RandomAccessFile memoryMappedFile = new RandomAccessFile(fn, "rw");
       
		    //Mapping a file into memory
	        MappedByteBuffer out = memoryMappedFile.getChannel().map(FileChannel.MapMode.READ_WRITE, 0, mem_map_size);
	      
	        //Writing into Memory Mapped File
	        for (int i = 0; i < mem_map_size; i++) {
	            out.put((byte) 'A');
	        }
	        System.out.println("File '" + fn + "' is now " + Integer.toString(mem_map_size) + " bytes full.");
	      
	        // Read from memory-mapped file.
	        for (int i = 0; i < 30 ; i++) {
	            System.out.print((char) out.get(i));
	        }
	        System.out.println("\nReading from memory-mapped file '" + fn + "' is complete.");
	   }
	}
The small model in Listing 3 quickly creates a 20-megabyte file, `example_memory_mapped_file.txt`, fills the file with the character _A_, then reads the first 30 bytes of the file. In practical cases, memory mapping is interesting not only for the raw speed of I/O, but also because several different readers and writers can attach simultaneously to the same file image. This technique is powerful enough to be dangerous, but in the right hands it makes for exceedingly fast implementations.

#### Character encoding and searching
This is particularly valuable for searches that must be sensitive to the encoding, collation, and other characteristics of languages other than English.

An example of a conversion from Java's native Unicode character encoding to Latin-1.

    String someString = "This is a string that Java natively stores as Unicode.";
    Charset latin1Charset = Charset.forName("ISO-8859-1");
    CharsetEncode latin1Encoder = charset.newEncoder();
    ByteBuffer latin1Buffer = latin1Encoder.encode(CharBuffer.wrap(some_string));


Note that  `Charset`s and channels are designed to work well together in order to ensure that programs requiring cooperation between memory mapping, asynchronous I/O, and encoding translation perform adequately.
