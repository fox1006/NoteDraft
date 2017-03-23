https://tools.ietf.org/html/rfc4648
因为有些数据传输由于遗留系统的影响，只接受us-asill编码字符，所以将数据用base编码编译成us-asill字符，现在也可以利用base编码来便于文本编辑器操作对象
每24位字节，base64切换成4个6位字节，然后根据表格转换
比如:
这
-24, -65, -103
11101000 10111111 10011001
111010001011111110011001
6L+Z
58,11,62,25
00111010 00001011 00111110 00011001
111010 001011 111110 011001
111010001011111110011001

不到24位字节，右边补零到24，再切换4个6位字节，根据表格转换，但是右边的补零每6个字节以=代替
T
84
01010100 -> 010101000000000000000000
010101 000000 000000 000000
21, 0, =, =
VA==

base64里+和/在url里有特殊含义，所以如果要给url里参数做编码的话，须使用-和_来替换这两个符号

jdk8里的java.util.Base64.Encoder的功能是和sun.misc.BASE64Encoder一样的，但是后者是非公开类所以以后版本jdk也许会删除；所以尽量使用前者。

老版本jdk的话还是使用apache提供的方法比较保险。  


``` java

	/**
	 * Use java.util.Base64.Encoder to encode source string;
	 * and use java.util.Base64.Decoder to decode encoded string.
	 * @param src source string
	 */
	private static void encode(final String src) {
		System.out.println("----------java.util.Base64-----------");
		try {
			byte[] srcByteArray;
			Encoder encoder = java.util.Base64.getEncoder();
			Decoder decoder = java.util.Base64.getDecoder();
			
			srcByteArray = src.getBytes("UTF-8");
			String desc = encoder.encodeToString(srcByteArray);
			
			System.out.println("Source string=" + src + "\r\n" + "Encoded string=" + desc);
		
			srcByteArray = decoder.decode(desc);
			desc = new String(srcByteArray, "UTF-8");
			
			System.out.println("Decoded string=" + desc);
		} catch (UnsupportedEncodingException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
	
	/**
	 * Use sun.misc.BASE64Encoder to encode source string;
	 * and use sun.misc.BASE64Decoder to decode encoded string
	 * @param src source string
	 */
	private static void encodeBySun(final String src) {
		System.out.println("----------BASE64Encoder-----------");
		try {
			byte[] srcByteArray;
			BASE64Encoder encoder = new BASE64Encoder();
			BASE64Decoder decoder = new BASE64Decoder();
			
			srcByteArray = src.getBytes("UTF-8");
			String desc = encoder.encode(srcByteArray);
			
			System.out.println("Source string=" + src + "\r\n" + "Encoded string=" + desc);
		
			srcByteArray = decoder.decodeBuffer(desc);
			desc = new String(srcByteArray, "UTF-8");
			
			System.out.println("Decoded string=" + desc);
		} catch (UnsupportedEncodingException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}

``` 
