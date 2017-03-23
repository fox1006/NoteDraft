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
