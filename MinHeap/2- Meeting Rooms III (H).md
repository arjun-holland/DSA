# Problem
<img width="1163" height="503" alt="image" src="https://github.com/user-attachments/assets/8752c7fd-361b-4750-a4c4-e8a36f5bdab3" />

<img width="655" height="602" alt="image" src="https://github.com/user-attachments/assets/f5656bcb-ded2-4806-b7ec-3f557b6b4e5e" />

<img width="714" height="315" alt="image" src="https://github.com/user-attachments/assets/cb753a67-d2ba-4cc8-97f8-7e5637f7f87e" />

# Intuition : Its a simple simulation process
```
  -Sort the meetings as start time < end time for all meetings 
  -Find the available room
      -If room find then use that room and increase that room used count
      -If room not find then use the room which has lowest end meeting time
  -Find the mostly used room and return that room number
```

# Brute-Force Code
```
class Solution {
public:
    int mostBooked(int n, vector<vector<int>>& meetings) {
        int m = meetings.size();

        sort(begin(meetings), end(meetings));       //sort by starting time of meetings

        vector<int> roomsUsedCount(n, 0);            //Each room is used 0 times in the beginning
        vector<long long> lastAvailableAt(n, 0);    //Each room will be last available at
        

        for(vector<int>& meet : meetings) {
            int start  = meet[0];
            int end    = meet[1];
            bool found = false;

            long long EarlyEndRoomTime = LLONG_MAX;
            int EarlyEndRoom     = 0;

            for(int room = 0; room < n; room++) {           //Find the first available meeting room
                if(lastAvailableAt[room] <= start) {
                    found = true;
                    lastAvailableAt[room] = end;
                    roomsUsedCount[room]++;
                    break;
                }

                if(lastAvailableAt[room] < EarlyEndRoomTime) {
                    EarlyEndRoom = room;
                    EarlyEndRoomTime = lastAvailableAt[room];
                }
            }

            if(!found) {
                lastAvailableAt[EarlyEndRoom] += (end - start);  //keep the meeting in this room
                roomsUsedCount[EarlyEndRoom]++;
            }

        }

        int resultRoom = -1;
        int maxUse     = 0;  
        for(int room = 0; room < n; room++) {
            if(roomsUsedCount[room] > maxUse) {
                maxUse = roomsUsedCount[room];
                resultRoom = room;
            }
        }

        return resultRoom;
    }
};
```
<img width="1122" height="470" alt="image" src="https://github.com/user-attachments/assets/acdaf634-79f5-4f39-8ae3-02b69fff1a15" />

# Intuition
```
    -When we observe the Brute force we got that we have taken the early available room always (least meeting ender time).
    -With what data structure we can take the early available room always , which is nothing but min heap (a container which give the min value among all the values that the container has).
    -We have the take the first available room if multiple rooms are available so keep the available rooms in the another min heap so that we can take the least available room always.
```

# Optmized Code
```
typedef pair<long long, int> P;
class Solution {
public:

    int mostBooked(int n, vector<vector<int>>& meetings) {
        int m = meetings.size();
        sort(begin(meetings), end(meetings)); //sort by starting time of meetings

        vector<int> roomsUsedCount(n, 0);     //Each room is used 0 times in the beginning
        priority_queue<P, vector<P>, greater<P>> usedRooms;  //To store {earliest room empty time, room No.}
        priority_queue<int, vector<int>, greater<int>> unusedRooms;   //To store rooms that are not used

        for(int room = 0; room < n; room++) {
            unusedRooms.push(room);             //All rooms are unused in the beginning
        }

        for(vector<int>& meet : meetings) {
            int start  = meet[0];
            int end    = meet[1];

            //First see, by this time, which rooms can be empty now, And move them to unusedRooms
            while(!usedRooms.empty() && usedRooms.top().first <= start) {
                int room = usedRooms.top().second;
                usedRooms.pop();
                unusedRooms.push(room);
            }

            if(!unusedRooms.empty()) {
                int room = unusedRooms.top();
                unusedRooms.pop();
                usedRooms.push({end, room});
                roomsUsedCount[room]++;
            } else {           //We don't have any room available now. Pick earliest end room
                int room          = usedRooms.top().second;
                long long endTime = usedRooms.top().first;
                usedRooms.pop();
                usedRooms.push({endTime + (end-start), room});
                roomsUsedCount[room]++;
            }

        }

        int resultRoom = -1;
        int maxUse     = 0;  
        for(int room = 0; room < n; room++) {
            if(roomsUsedCount[room] > maxUse) {
                maxUse = roomsUsedCount[room];
                resultRoom = room;
            }
        }

        return resultRoom;
    }
};
```
<img width="1097" height="517" alt="image" src="https://github.com/user-attachments/assets/1baa6d5d-d6c0-4965-9397-c74cd9ed2312" />

<img width="1198" height="560" alt="image" src="https://github.com/user-attachments/assets/3a71d43d-3572-4635-860a-70cb59247b12" />

<img width="965" height="290" alt="image" src="https://github.com/user-attachments/assets/39c1e1a3-2bad-48b0-bb7c-ed9d6774a8f4" />

