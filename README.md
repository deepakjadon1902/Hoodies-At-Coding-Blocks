import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        int Q = scanner.nextInt();  // Number of queries
        
        // Main queue to maintain the order of courses
        Queue<Integer> mainQueue = new LinkedList<>();
        // HashMap to maintain the queue of students for each course
        HashMap<Integer, Queue<Integer>> courseQueues = new HashMap<>();
        // Set to keep track of which course is currently in the main queue
        Set<Integer> courseInQueue = new HashSet<>();
        
        for (int i = 0; i < Q; i++) {
            String operation = scanner.next();
            
            if (operation.equals("E")) {
                int course = scanner.nextInt();
                int rollNumber = scanner.nextInt();
                
                // If course queue doesn't exist, create it
                courseQueues.putIfAbsent(course, new LinkedList<>());
                
                // Enqueue the student in their course queue
                courseQueues.get(course).add(rollNumber);
                
                // If the course is not already in the main queue, add it
                if (!courseInQueue.contains(course)) {
                    mainQueue.add(course);
                    courseInQueue.add(course);
                }
            } else if (operation.equals("D")) {
                // Dequeue the student from the course queue which is at the front of the main queue
                int frontCourse = mainQueue.peek();
                int rollNumber = courseQueues.get(frontCourse).poll();
                
                System.out.println(frontCourse + " " + rollNumber);
                
                // If the course queue is empty, remove it from the main queue and the set
                if (courseQueues.get(frontCourse).isEmpty()) {
                    mainQueue.poll();
                    courseInQueue.remove(frontCourse);
                }
            }
        }
        
        scanner.close();
    }
}
