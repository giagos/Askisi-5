# Askisi-5

Σε αυτή την άσκηση πρέπει να δημιουργήσετε ένα σύστημα που θα ενσωματωθεί σε ένα κουτί με φάρμακα για ηλικιωμένους που ξεχνούν πότε
πρέπει να τα πάρουν.
 
Εδώ θα φτιάξουμε μια προσομείωση του παραπάνω συστήματος, ώστε μετά να μπορείτε να το δημιουργήσετε με πραγματικά υλικά.
 
Θα χρησιμοποιηθούν κάποιοι αισθητήρες οι οποίοι ανιχνεύουν κλήση, που θα τους λέμε tilt sensors. Τα tilt sensors εάν κουνηθούν αλλάζουν την
τιμή τους. Εάν είναι 0 σε 1 και εάν είναι 1 σε 0. Δεν μπορούμε να γνωρίζουμε εκ των προτέρων τι τιμή έχουν σε κάθε θέση, άρα πρέπει απλά να
κοιτάμε εάν η τιμή τους έχει αλλάξει ανάμεσα σε δύο χρονικές στιγμές.
 
Ένα άλλο σημαντικό στοιχείο αυτής της άσκησης, είναι ότι δε θα χρησιμοποιήσουμε delays ώστε να εκτελέσουμε κάποιες εντολές σε μια
συγκεκριμένη συχνότητα. Αν θυμάστε, πριν αναβοσβήναμε ένα λαμπάκι κάθε ένα δευτερόλεπτο, ανάβοντας το λαμπάκι, σταματώντας την εκτέλεση
του προγράμματος για 1 δευτερόλεπτο, σβήνοντας το λαμπάκι και σταματώντας την εκτέλεση του προγράμματος για ένα δευτερόλεπτο.
Επειδή σε αυτή την περίπτωση δεν έχουμε την πολυτέλεια να σταματήσουμε την εκτέλεση του προγράμματος (διότι πρέπει να κοιτάμε ανά πάσα
στιγμή εάν έχει ανοίξει το καπάκι) θα χρησιμοποιήσουμε μια διαφορετική και πολύ χρήσιμη τακτική. Θα ελέγχουμε σε ένα if, εάν έχει περάσει
ένας συγκεκριμένος χρόνος για παράδειγμα 5 δευτερόλεπτα, από την τελευταία φορά που μπήκαμε στο συγκεκριμένο if. Για αυτό το σκοπό, θα
χρησιμοποιήσουμε την εντολή millis() η οποία επιστρέφει τα πόσα μιλισεκόντ έχουν περάσει απ' τη στιγμή που ξεκίνησε τη λειτουργία του
το Arduino.
 
Για παράδειγμα, μελετήστε τον παρακάτω κώδικα:
 
 void loop(){
   unsigned long now = millis(); //αποθηκεύει στη μεταβλητή now το πόσα μιλλισεκοντ έχουν περάσει απ' την έναρξη λειτουργίας του arduino
   if (now >= lastTime + 5000){ //ΑΝ τώρα έχουν περάσει περισσότερα από 5000 μιλλισεκόντ σε σχέση με την προηγούμενη φορά, τότε μπες στο if
     //κάνε κάτι
   	 lastTime = now; //η τωρινή στιγμή αποθηκεύεται ως "η τελευταία φορά", ώστε η επόμενη είσοδος στο if να γίνει 5000 μιλισεκόντ αργότερα
   }
 }
 
Ο κώδικας που βρίσκεται μέσα στο παραπάνω if, εκτελείται κάθε 5 δευτερόλεπτα. Μην ξεχνάτε να αποθηκεύσετε πότε έγινε η τελευταία είσοδος στο if,
διότι εάν δεν το κάνετε, τότε ο κώδικας θα εκτελείται συνεχώς μετά τα πρώτα 5 δευτερόλεπτα. Άρα θα πρέπει να σκεφτούμε ως εξής:
1. Αποθηκεύουμε την τωρινή χρονική στιγμή (π.χ. έχουν περάσει 10 δευτερόλεπτα απ' την εκκίνηση του προγράμματος)
2. Ελέγχουμε εάν η τωρινή χρονική στιγμή, είναι μεγαλύτερη η ίση σε σχέση με την τελευταία χρονική στιγμή που μπήκαμε στο if ΣΥΝ τη συχνότητα.
 Εάν η τελευταία φορά που μπήκαμε στο if ήταν στα 8 δευτερόλεπτα, σημαίνει ότι δεν είναι ο καιρός για να ξαναμπούμε. Διότι το 10 ΔΕΝ είναι
 μεγαλύτερο ή ίσο σε σχέση με το 8 δευτερόλεπτα (όπου ήταν η τελευταία είσοδος) ΣΥΝ 5, το οποίο είναι η συχνότητά μας.
3. Εκτελούμε τον κώδικα.
4. Αποθηκεύουμε την τωρινή χρονική στιγμή, στη μεταβλητή που αντιπροσωπεύει την "τελευταία φορά" που μπήκαμε στο if, ώστε η επόμενη φορά που
θα ξαναμπούμε να είναι 5 δευτερόλεπτα αργότερα.

Συνοψίζοντας, η συνολική λογική του προγράμματος είναι η εξής:

1. Κάθε ένα συγκεκριμένο χρονικό διάστημα (INTERVAL) άνοιξε το λαμπάκι στο καπάκι του οποίου είναι η σειρά να ανοίξει.
2. Διάβασε την τιμή που δίνει το tilt sensor στο συγκεκριμένο καπάκι
3. Ξεκίνα να χτυπάς τον βομβητή
4. Εάν (σε οποιαδήποτε στιγμή) ο βομβητής χτυπάει, διάβασε την είσοδο του tilt sensor που βρίσκεται στο καπάκι που πρέπει να ανοίξει
5. Εάν η τιμή που διαβάσαμε τώρα, είναι διαφορετική της τιμής που είχαμε διαβάσει όταν ξεκινήσαμε να χτυπάμε το βομβητή, τότε
  σημαίνει πως το καπάκι έχει ανοίξει και άρα πρέπει να σταματήσουμε να χτυπάμε το βομβητή και να κλείσουμε οποιοδήποτε λαμπάκι είναι ανοιχτό.
6. Εάν ο χρήστης ανοίξει το καπάκι, μετά ορίζουμε το επόμενο καπάκι, ως το κατάλληλο που πρέπει να ανοιχθεί όταν έρθει η ώρα.

Δώστε ΜΕΓΑΛΗ ΠΡΟΣΟΧΗ, στην στοίχιση που βρίσκονται τα σχόλια, διότι αυτά υποδηλώνουν τα μπλοκ κώδικα που μπαίνουν μέσα στα if. ΜΗΝ σβήσετε
τα σχόλια και ακολουθείτε πιστά τις οδηγίες τους. Σε κάθε κενή γραμμή ανάμεσα τα σχόλια, μπαίνει και μια γραμμή κώδικα. Με λίγα λόγια, στο
τέλος ΔΕΝ πρέπει να υπάρχουν κενές γραμμές ανάμεσα στα σχόλια.
