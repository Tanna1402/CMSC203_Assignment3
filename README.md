# CMSC203_Assignment3
class CryptoManager {
  static int LOWER_BOUND = 32;
  static int UPPER_BOUND = 95;
  static int RANGE = UPPER_BOUND - LOWER_BOUND + 1;
  public static boolean stringInBounds(String plainText) {
    boolean flag = true;
    for (int i = 0; i < plainText.length(); i++) {
      if ( !((int) plainText.charAt(i) >= LOWER_BOUND && (int) plainText.charAt(i) <= UPPER_BOUND)) 
      { 
    	//false if any character is outside the bounds
        flag = false;
        break;
      }
    }

    //returns true if all characters are within the allowable bounds
    return flag;
  }

  public static String encryptCaesar(String plainText, int key) {
	  
    //Wrap around the key, if it is greater than the UPPER_BOUND
    key = Wrap_around(key);

    //encrypted text
    String encryptedText = "";

    if (stringInBounds(plainText))
    {
    	for (int i=0; i<plainText.length(); i++)
    	{
    		char thisChar = plainText.charAt(i);
    		int encryptedCharint = ((int)thisChar+key);
    		while (encryptedCharint > UPPER_BOUND)
    		{
    			encryptedCharint -= RANGE;
    		}
    		encryptedText += (char)encryptedCharint;
    	}
    }
    return encryptedText;
    }

  public static String decryptCaesar(String encryptedText, int key) {
	  
    //Wrap around the key, if it is greater than the UPPER_BOUND
    key = Wrap_around(key);

    //decrypted text
    String decryptedText = "";
    for (int i =0; i < encryptedText.length(); i++)
    {
    	char thisChar = encryptedText.charAt(i);
    	int decryptedCharint = ((int)thisChar-key);
    	decryptedText += (char)decryptedCharint;
    }
    return decryptedText;
   }

  public static int Wrap_around(int key) {
    while (key > UPPER_BOUND) {
      key -= (UPPER_BOUND - LOWER_BOUND);
    }

    return key;
  }

  public static String encryptBellaso(String plainText, String bellasoStr) {
    //encrypted text

	  String encryptedText = "";
	  int bellasoStrLength = bellasoStr.length();
	  for (int i = 0; i < plainText.length(); i++)
	  {
		  char thisChar = plainText.charAt(i);
		  int encryptedCharint = ((int)thisChar+(int)bellasoStr.charAt(i));
		  while (encryptedCharint > (int)UPPER_BOUND)
		  {
			  encryptedCharint -= RANGE;
		  }
		  encryptedText += (char)encryptedCharint;
	  }
	  return encryptedText;
  }
  

  public static String decryptBellaso(String encryptedText, String bellasoStr) {
    //decrypted text

	String decryptedText = "";
	int bellasoStrLength = bellasoStr.length();
	for (int i = 0; i < encryptedText.length(); i++)
	{
		char thisChar = encryptedText.charAt(i);
		int decryptedCharint = ((int)thisChar-(int)bellasoStr.charAt(i));
		while (decryptedCharint < (int)LOWER_BOUND)
		{
			decryptedCharint += RANGE;
		}
		decryptedText += (char)decryptedCharint;
	}
	return decryptedText;
  }
