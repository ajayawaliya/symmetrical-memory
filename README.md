# symmetrical-memory
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import java.util.Arrays;

public class KDFExample {

    public static byte[] deriveKey(byte[] secret, String context) throws Exception {
        Mac mac = Mac.getInstance("HmacSHA256");
        mac.init(new SecretKeySpec(secret, "HmacSHA256"));
        return mac.doFinal(context.getBytes());
    }

    public static void main(String[] args) throws Exception {
        byte[] secret = "sharedsecret".getBytes();

        byte[] forwardKey = deriveKey(secret, "forward");
        byte[] backwardKey = deriveKey(secret, "backward");

        System.out.println("Forward key length: " + forwardKey.length);
        System.out.println("Backward key length: " + backwardKey.length);
    }
}
