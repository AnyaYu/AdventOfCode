fun main(args: Array<String>) {
var MyString = "L5, R1, R3, L4, R3, R1, L3, L2, R3, L5, L1, L2, R5, L1, R5, R1, L4, R1, R3, L4, L1, R2, R5, R3, R1, R1, L1, R1, L1, L2, L1, R2, L5, L188, L4, R1, R4, L3, R47, R1, L1, R77, R5, L2, R1, L2, R4, L5, L1, R3, R187, L4, L3, L3, R2, L3, L5, L4, L4, R1, R5, L4, L3, L3, L3, L2, L5, R1, L2, R5, L3, L4, R4, L5, R3, R4, L2, L1, L4, R1, L3, R1, R3, L2, R1, R4, R5, L3, R5, R3, L3, R4, L2, L5, L1, L1, R3, R1, L4, R3, R3, L2, R5, R4, R1, R3, L4, R3, R3, L2, L4, L5, R1, L4, L5, R4, L2, L1, L3, L3, L5, R3, L4, L3, R5, R4, R2, L4, R2, R3, L3, R4, L1, L3, R2, R1, R5, L4, L5, L5, R4, L5, L2, L4, R4, R4, R1, L3, L2, L4, R3"
var List = MyString.split(", ");

   
    var StartPoint: Point = Point(0, 0);
    
   
  
    var LetterList = List.joinToString("").split("[0-9]".toRegex());
    LetterList = LetterList.filterNot({it.equals("")});
    
    var NumberList =  List.joinToString("").split("[L,R]".toRegex());
    NumberList = NumberList.takeLast(NumberList.size-1);

    
       
    fun direction (Currentd: String, move: String): String{
        var NewCurrentd = Currentd;
        if (NewCurrentd == "n" && move == "R") NewCurrentd = "e";
        else if (NewCurrentd == "e" && move == "R") NewCurrentd = "s";
        else if (NewCurrentd == "s" && move == "R") NewCurrentd = "w";
        else if (NewCurrentd == "w" && move == "R") NewCurrentd = "n";
        else if (NewCurrentd == "n" && move == "L") NewCurrentd = "w";
        else if (NewCurrentd == "e" && move == "L") NewCurrentd = "n";
        else if (NewCurrentd == "s" && move == "L") NewCurrentd = "e";
        else if (NewCurrentd == "w" && move == "L") NewCurrentd = "s";
        return NewCurrentd;
    }
    

    fun EndPoint (StartP: Point, LetterL: List<String>, NumberL: List<String>): Point{
        var d = "n"
        for (i in LetterL.indices){
           d = direction (d, LetterL.get(i))
            if (d == "n"){
                StartP.y += NumberL.get(i).toInt();             
            }
            if (d == "e"){
                StartP.x += NumberL.get(i).toInt();             
            }
             if (d == "s"){
                StartP.y -= NumberL.get(i).toInt();             
            }
             if (d == "w"){
                StartP.x -= NumberL.get(i).toInt();             
            }
        
    }
        var EndPoint = StartP;
        return EndPoint;
    }
    

    print (EndPoint (StartPoint, LetterList, NumberList));
}

 data class Point (var x: Int, var y: Int);
