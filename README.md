# 250711-
Console - Text RPG (스파르타 던전) 과제

using System;

class Program
{
   static void Main()
    { 
        int[] player = new int[6];
        player[0] = 1;
        player[1] = 0;
        player[2] = 10;
        player[3] = 5;
        player[4] = 100;
        player[5] = 15000;

        string[] job = new string[4];
        job[0] = "전사";
        job[1] = "궁수";
        job[2] = "마법사";
        job[3] = "도적";

        List<List<int>> item = new List<List<int>>(); //방어는 1 공격은 0
        item.Add(new List<int> { 0, 1, 5, 1000 });
        item.Add(new List<int> { 1, 1, 9, 2000 });
        item.Add(new List<int> { 2, 1, 15, 3500 });
        item.Add(new List<int> { 3, 0, 2, 600 });
        item.Add(new List<int> { 4, 0, 5, 1500 });
        item.Add(new List<int> { 5, 0, 7, 3000 });

        List<List<string>> itemName = new List<List<string>>();
        itemName.Add(new List<string> {"수련자 갑옷","수련에 도움을 주는 갑옷입니다."});
        itemName.Add(new List<string> {"무쇠갑옷","무쇠로 만들어져 튼튼한 갑옷입니다."});
        itemName.Add(new List<string> {"스파르타의 갑옷", "스파르타의 전사들이 사용했다는 전설의 갑옷입니다."});
        itemName.Add(new List<string> {"낡은 검", "쉽게 볼 수 있는 낡은 검 입니다."});
        itemName.Add(new List<string> {"청동 도끼", "어디선가 사용됐던거 같은 도끼입니다."});
        itemName.Add(new List<string> {"스파르타의 창", "스파르타의 전사들이 사용했다는 전설의 창입니다."});

        List<int> inventory = new List<int>();

        //List<int> itemList = new List<int>();

        while (true)
        {
            Console.WriteLine("\n스파르타 마을에 오신 여러분 환영합니다.\n이곳에서 던전으로 들어가기전 활동을 할 수 있습니다.");
            Console.WriteLine("\n1. 상태 보기\n2. 인벤토리\n3. 상점");
            Console.Write("\n원하시는 행동을 입력해주세요.\n>>");
            string input = Console.ReadLine();
            Console.Clear();

            switch (input)
            {
                case "1":
                    while (true)
                    {
                        Console.WriteLine("\n상태 보기\n캐릭터의 정보가 표시됩니다.\n");
                        Console.WriteLine("Lv. {0:D2}", player[0]);
                        Console.WriteLine("Chad " + "( " + job[player[1]] + " )");
                        Console.WriteLine("공격력 : " + player[2]);
                        Console.WriteLine("방어력 : " + player[3]);
                        Console.WriteLine("체  력 : " + player[4]);
                        Console.WriteLine("Gold : " + player[5] + " G");
                        Console.WriteLine("\n0. 나가기\n");
                        Console.Write("원하시는 행동을 입력해주세요.\n>>");
                        if (Console.ReadLine() == "0") break;
                    }
                    break;
                case "2":
                    while (true)
                    {
                        Console.WriteLine("\n인벤토리\n보유 중인 아이템을 관리할 수 있습니다.");
                        Console.WriteLine("\n[아이템 목록]\n");

                        if(inventory.Count == 0)
                        {
                            Console.WriteLine("아이템이 없습니다.");
                        }
                        else
                        {
                            foreach (int itemId in inventory)
                            {
                                List<int> itemData = item.Find(x => x[0] == itemId);
                                string name = itemName[itemId][0];
                                string data = itemName[itemId][1];
                                string type = itemData[1] == 0 ? "공격력" : "방어력";
                                int value = itemData[2];

                                Console.WriteLine($"- {name} | {type} + {value} | {data}");
                            }
                        }

                        Console.WriteLine("\n1. 장착 관리\n0. 나가기\n");
                        Console.WriteLine("원하시는 행동을 입력해주세요.");
                        Console.Write(">>");
                        string itemCheck = Console.ReadLine();
                        Console.Clear();
                        if (itemCheck == "0") break;

                        else if (itemCheck == "1")
                        {
                            while (true)
                            {
                                int itemIndex = 1;
                                Console.WriteLine("\n인벤토리\n보유 중인 아이템을 관리할 수 있습니다.");
                                Console.WriteLine("\n[아이템 목록]\n");

                                if (inventory.Count == 0)
                                {
                                    Console.WriteLine("아이템이 없습니다.");
                                }
                                else
                                {
                                    foreach (int itemId in inventory)
                                    {
                                        List<int> itemData = item.Find(x => x[0] == itemId);
                                        string name = itemName[itemId][0];
                                        string data = itemName[itemId][1];
                                        string type = itemData[1] == 0 ? "공격력" : "방어력";
                                        int value = itemData[2];

                                       
                                    }
                                }

                                Console.WriteLine("\n0. 나가기\n");
                                Console.WriteLine("원하시는 행동을 입력해주세요.");
                                Console.Write(">>");
                               
                                if (Console.ReadLine() == "0") break;
                            }
                        }
                    }
                    break;
                case "3":
                    while (true)
                    {
                        Console.WriteLine("\n상점\n필요한 아이템을 얻을 수 있는 상점입니다.\n");
                        Console.WriteLine("[보유 골드]");
                        Console.WriteLine(player[5] + "G\n");
                        Console.WriteLine("[아이템 목록]");

                        foreach (List<int> itemList in item)
                        {
                            Console.WriteLine($"- {itemName[itemList[0]][0],-10} | {(itemList[1] == 0 ? "공격력" : "방어력")} + {itemList[2]}  | {itemName[itemList[0]][1],-40} | {(itemList[3] == 0 ? "구매완료" : itemList[3] + "G")}");
                        }

                        Console.WriteLine("\n1. 아이템 구매\n0. 나가기\n");
                        Console.WriteLine("원하시는 행동을 입력해주세요.");
                        Console.Write(">>");
                        string storeCheck = Console.ReadLine();
                        Console.Clear();
                        if (storeCheck == "0") break;

                        else if (storeCheck == "1")
                        {
                            while (true)
                            {
                                int storeIndex = 1;
                                Console.WriteLine("\n상점\n필요한 아이템을 얻을 수 있는 상점입니다.\n");
                                Console.WriteLine("[보유 골드]");
                                Console.WriteLine(player[5] + "G\n");
                                Console.WriteLine("[아이템 목록]");

                                foreach (List<int> itemList in item)
                                {
                                    Console.WriteLine($"- {storeIndex} {itemName[itemList[0]][0],-10} | {(itemList[1] == 0 ? "공격력" : "방어력")} + {itemList[2]}  | {itemName[itemList[0]][1],-40} | {(itemList[3] == 0 ? "구매완료" : itemList[3] + "G")}");
                                    storeIndex++;
                                }

                                Console.WriteLine("\n0. 나가기\n");
                                Console.WriteLine("원하시는 행동을 입력해주세요.");
                                Console.Write(">>");
                                string buyCheck = Console.ReadLine();
                                Console.Clear();
                                if (buyCheck == "0") break;
                                else
                                {
                                    int buyNum = int.Parse(buyCheck) - 1;

                                    if (buyNum >= 0 && buyNum < item.Count)
                                    {
                                        if (item[buyNum][3] == 0)
                                            Console.WriteLine("이미 구매한 아이템입니다.");
                                        else if (item[buyNum][3] > player[5])
                                        {
                                            Console.WriteLine("Gold가 부족합니다.");
                                        }
                                        else
                                        {
                                            player[5] -= item[buyNum][3];
                                            item[buyNum][3] = 0;
                                            inventory.Add(item[buyNum][0]);
                                            Console.WriteLine("구매를 완료했습니다.");
                                        }
                                    }
                                    else
                                    {
                                        Console.WriteLine("\n잘못된 입력입니다.\n");
                                    }
                                }

                            }
                        }
                    }
                    break;
                    default:
                    Console.WriteLine("\n잘못된 입력입니다.\n");
                    break;
            } 
        }
    }
}
