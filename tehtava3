import java.sql.*;
import java.util.Random;

/**
 *
 * @author miklas
 */
public class Tietokantatesti {

    /**
     * @param args the command line arguments
     * @throws java.sql.SQLException
     */
    public static void main(String[] args) throws SQLException {

        Connection db = DriverManager.getConnection("jdbc:sqlite:testi.db");
        Statement trs = db.createStatement();
        Random randomi = new Random();
        ///////////////////////
        //// laita aina boolean arvo todeksi ja muut epätodeksi alas jos haluat ajaa tiettyä testiä
        boolean testi1 = false;
        boolean testi2 = false;
        boolean testi3 = true;
        ///////////////////////
        String k = "";
        int x = 0;
        int y = 0;
        long bc = 0;
        long ba = 0;
        long minus = 0;
        long alkuaika = 0;
        long loppuaika = 0;

        trs.execute("CREATE TABLE Elokuvat (id INTEGER PRIMARY KEY, nimi TEXT, vuosi INTEGER);");
        trs.execute("BEGIN");

        if (testi2 && !testi1 && !testi3) {
            trs.execute("CREATE INDEX index_el on Elokuvat (vuosi)");
        }

        alkuaika = System.nanoTime();
        while (x < 1000000) {

            k = "";
            y = 0;
            bc = System.nanoTime();
            while (y < 10) {
                k += (char) (randomi.nextInt(26) + 'a');
                y++;
            }
            ba = System.nanoTime();
            minus += ba - bc;
            PreparedStatement nimi = db.prepareStatement("INSERT INTO Elokuvat (nimi, vuosi) VALUES (?, ?);");
            nimi.setString(1, k);
            nimi.setInt(2, randomi.nextInt((2000 - 1900) + 1) + 1900);
            nimi.executeUpdate();
            x++;
        }
        trs.execute("COMMIT");
        loppuaika = System.nanoTime();
        System.out.println("Rivien lisäämiseen kuluva aika: " + (loppuaika - alkuaika - minus) / (double) 1000000000 + " sekuntia");
        x = 0;

        if (testi3 && !testi2 && !testi1) {
            trs.execute("CREATE INDEX index_el on Elokuvat (vuosi)");
        }

        alkuaika = System.nanoTime();
        while (x < 1000) {

            try {

                PreparedStatement vuosihaku = db.prepareStatement("SELECT COUNT(*) FROM Elokuvat WHERE Vuosi = ?");
                vuosihaku.setInt(1, randomi.nextInt((2000 - 1900) + 1) + 1900);
                vuosihaku.executeQuery();

            } catch (SQLException e) {
                System.out.println(e);
            }
            x++;

        }
        loppuaika = System.nanoTime();
        System.out.println("Kyselyiden suoritukseen kuluva aika: " + (loppuaika - alkuaika) / (double) 1000000000 + " sekuntia");

    }
