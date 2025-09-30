#projekts "GitKaulins"

![Metamā kauliņa attels](https://pngimg.com/uploads/dice/dice_PNG49.png)


**Darāmo darbu saraksts**
-[x] Uzsākta lokāla Java projekta versionēšana ar Git
-[x]Izveidots GitHub konts
-[x]Izveidota GitHub krātuve (repo)
-[x]Lokālā projekta versija izvietota GitHub
-[ ]Projektam pieslēdzies vēl viens programmētājs un izmēģinata kopdarbošanās
-[ ]Projektā ievests jauns zars (branch)
-[ ] Sapludināti zari un noversts merge konflikts
-[ ] Izmeģināts pull request



package OOP;

import java.time.Year;
import java.util.regex.Pattern;
import javax.swing.JOptionPane;

public class MinkuTante {

    static String virknesParbaude(String zinojums, String noklusejums) {
        String virkne;
        do {
            virkne = JOptionPane.showInputDialog(zinojums, noklusejums);
            if (virkne == null) return null;
        } while (!Pattern.matches("^[\\p{L} ]+$", virkne));
        return virkne;
    }

    public static int skaitlaParbaude(String zinojums, int min, int max) {
        String ievade;
        int skaitlis;
        while (true) {
            ievade = JOptionPane.showInputDialog(null, zinojums, "Datu ievade", JOptionPane.INFORMATION_MESSAGE);
            if (ievade == null) return -1;

            try {
                skaitlis = Integer.parseInt(ievade);
                if (skaitlis < min || skaitlis > max) {
                    JOptionPane.showMessageDialog(null, "Noradits nekorets intervals", "Nekorekti dati", JOptionPane.WARNING_MESSAGE);
                    continue;
                }
                return skaitlis;
            } catch (NumberFormatException e) {
                JOptionPane.showMessageDialog(null, "Netika ievadits vesels skaitlis", "Nekorekti dati", JOptionPane.ERROR_MESSAGE);
            }
        }
    }

    public static void main(String[] args) {
        String izvele;
        oop runcis = null;
        String[] darbibusaraksts = {
            "Izveidot kaki", "Izsaukt metodes",
            "Saglabat faila", "Apskatit failu", "Apturet"
        };

        do {
            izvele = (String) JOptionPane.showInputDialog(null,
                "Izvelies darbibu", "Darbibu izvele",
                JOptionPane.QUESTION_MESSAGE, null, darbibusaraksts, darbibusaraksts[0]);

            if (izvele == null) izvele = "Apturet";

            switch (izvele) {
                case "Izveidot kaki":
                    String minkaVards = JOptionPane.showInputDialog("Ievadi kaka vardu", "Felikss");
                    String skirne = JOptionPane.showInputDialog("ievadi kaka skirne", "Meinkuns");
                    String spalvasKrasa = JOptionPane.showInputDialog("Iavedi kazoka krasu", "Melna");
                    String saimnieks = JOptionPane.showInputDialog("Ka sauc saimnieka", "Intars");
                    int dzGads = skaitlaParbaude("Noradi dzimsanas gadu", (Year.now().getValue()) - 15, Year.now().getValue());
                    int poga = JOptionPane.showConfirmDialog(null, "Vai kaķim ir sirsniņa?", "Kaķa sirsniņa",
                        JOptionPane.YES_NO_OPTION, JOptionPane.QUESTION_MESSAGE);
                    if (poga == -1) break;
                    boolean siksnina = (poga == 0);
                    String cels = virknesParbaude("Ievadi bildes nosaukumu un paplašinajumu", "kot1.png");

                    runcis = new oop(minkaVards, skirne, spalvasKrasa, saimnieks, dzGads, siksnina, cels);
                    break;

                case "Izsaukt metodes":
                    if (runcis != null) {
                        String[] metozuSaraksts = {
                            "Paglaudīt", "Nolasīt atribūtuts", "Pabarot", "Nolikt gulēt",
                            "Palielināt vecumu", "Apskatīt vecumu", "Medīt"
                        };

                        String metode = (String) JOptionPane.showInputDialog(null, "Izvelies metodi", "Metodes izvēle",
                            JOptionPane.QUESTION_MESSAGE, null, metozuSaraksts, metozuSaraksts[0]);
                        if (metode == null) return;

                        switch (metode) {
                            case "Paglaudīt":
                                runcis.murrat();
                                break;
                            case "Nolasīt atribūtuts":
                                JOptionPane.showMessageDialog(null, runcis.nolasitAtributus(), "Informacija", JOptionPane.INFORMATION_MESSAGE);
                                break;
                            case "Pabarot":
                                String atbilde = runcis.pabarot(virknesParbaude("Ar ko pabarot kaķi?","Desa"));
                                JOptionPane.showMessageDialog(null, "Kaķis atgriež "+atbilde, "Informācija", JOptionPane.INFORMATION_MESSAGE);                   
                                break;
                            case "Nolikt gulēt":
                            	String priksmets = virknesParbaude("Ko daosi kaķim uz gultiņu?", "Spilvens");
                                if(priksmets == null || priksmets.isEmpty())
                                	runcis.gulet();
                                
                                else
                                	runcis.gulet(priksmets);
                                break;
                            case "Palielināt vecumu":
                            	runcis.palielinatVecumu();
                                break;
                            case "Apskatīt vecumu":
                                runcis.nolasitVecumu();
                                break;
                            case "Medīt":
                                runcis.medit();
                                break;
                        }
                    } else {
                        JOptionPane.showMessageDialog(null, "Vispirms izveido kaķi!", "Kļume", JOptionPane.WARNING_MESSAGE);
                    }
                    break;

                case "Saglabat faila":
                	DarbsArFailu.saglabat(runcis);
                    break;

                case "Apskatit failu":
                	DarbsArFailu.nolasit();
                    break;

                case "Apturet":
                	JOptionPane.showMessageDialog(null, "Programma aptureta!", "Paziņojums",JOptionPane.INFORMATION_MESSAGE);
                    break;
            }
        } while (!izvele.equals("Apturet"));
    }
}
