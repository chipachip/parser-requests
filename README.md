
import java.io.*;
import java.net.*;
import java.util.*;
import java.util.regex.*;
import javax.management.*;


public class Solution {
    public static void main(String[] args) throws IOException {
    	ArrayList<String> values = new ArrayList<>(); //массив для добавления названий параметров
    	ArrayList<String> keys = new ArrayList<>(); //массив для добавления значений параметров  	
    	Map<String, String> map = new HashMap<>();//карта для хранения разбитой строки на название параметра и его значение
    	BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
    	String s = reader.readLine();
    	
    	URL url = new URL(s);
        String URL = url.getQuery();//вытаскиваем строку начинающуюся с символа '?'
        
        String[] params = URL.split("&");//создаём массив со строками разбитыми по заданному рег. выражению
        
        for (String param : params)  //проходим по массиву с разбитыми строками 
        {  
            String name = param.split("=")[0]; //отделяем названия параметров и добавляем в новый массив 
            values.add(name);
        } 
        
        String[] res = new String[values.size()];
        res = values.toArray(res); //преобразуем новый созданный массив с названиями параметров в строчный
   
        if(Arrays.asList(res).contains("obj") == true) { //проверяем есть ли параметр "obj" в массиве
        	for (String param : params)  //проходим по массиву с разбитыми строками
            {  
                String name = param.split("=")[0];  //добавляем название параметра как ключ
                String value = param.split("=")[1];  //добавляем содержимое параметра как значение
                keys.add(value); //отдельно добавляем значение в созданный массив
                map.put(name, value);  
            } 
        	
        	for(String name : map.keySet()) { //выводим через пробел названия параметров
        		System.out.print(name + " ");
        	}
        	
        	System.out.println();
        	
        	String pars = keys.get(0);
        	
        	try {
        		double dN = Double.parseDouble(pars); //парсим значение параметра obj в тип double
        		alert(dN); //если всё прошло успешно то применяем нужный нам метод
        	} catch (NumberFormatException e) {
        		alert(pars); //если выкинуто исключение то применяем другой метод, для String
        	}
        	
        } else { //если в массиве с названиями параметров нету параметра с именем obj
        	
        for(String name : values) {
        	System.out.print(name + " "); //выводим через пробел названия параметров
        }
        
        }
    }
     
    public static void alert(double value) {
        System.out.println("double: " + value);
    }

    public static void alert(String value) {
        System.out.println("String: " + value);
    }
}
