
namespace ConsoleApp3
{
    internal class Program
    {
        static void Main(string[] args)
        {
            double[] water_month = new double[12];
            double[] money_water = new double[12];

            Console.WriteLine("Please enter the customer type:   \n1. Household customer\n2. Administrative agency or public services\n3. Production units\n4. Business services\n");
            string client = Console.ReadLine() ?? string.Empty;
            Console.WriteLine(check_client(client));
            Console.WriteLine("Please enter the country number for the month 1 :");
            water_month[0] = Convert.ToInt32(Console.ReadLine());
            // dùng for để yêu cầu người nhập nhập số nước của các tháng 
            for (int i = 1; i <12; i++)
            {
                int this_month;
                do
                {
                    Console.WriteLine($"Enter the country number of the month {i + 1}");
                    this_month = Convert.ToInt32(Console.ReadLine());

                    // kiểm tra số nước tháng hiện tại phải lớn hơn tháng trước nếu không đúng sẽ báo lỗi và yêu cầu nhập lại 
                    if (this_month < water_month[i - 1])
                    {
                        Console.WriteLine("This month's water number must be greater than or equal to the previous month's water number");
                    }
                } while (this_month < water_month[i - 1]);

                water_month[i] = this_month; // Gán giá trị hợp lệ vào mảng
                double m3 = water_month[i] - water_month[i-1];
                money_water[i] = calculator(client, m3);
            }
            Console.WriteLine("Enter the month and want to know the water bill: ");
            int moth_want= Convert.ToInt32(Console.ReadLine());
            if (moth_want>= 1 && moth_want<=12 )
             {
                Console.WriteLine($" Number of countries per month {moth_want} is {water_month[moth_want-1]- water_month[moth_want-2 ]}");
                 Console.WriteLine($"water amount {moth_want} is {money_water[moth_want-1]}");
             }

        }


        static double calculator(string client , double m3)
        {
                double money_water = 0; 
            switch(client)
            {
                    case "Household customer":
                    case "1":
                        if (m3 <= 10)
                        {
                            money_water = m3 * 5.973;
                        }
                        else if (m3 <= 20)
                        {
                            money_water = (10 * 5.973) + (m3 - 10) * 7.052;
                        }
                        else if (m3 <= 30)
                        {
                            money_water =( 10 * 5.973 )+( 10 * 7.052 )+ (m3 - 20) * 8.699;
                        }
                        else
                        {
                            money_water = (10 * 5.973 )+( 10 * 7.052) + (10 * 8.699) + (m3 - 30) * 15.929;
                        }
                        break;

                case "Administrative agency":
                case "2":
                case "Public services":
                    money_water = m3 * 9.955;
                    break;
                case "Production units":
                case "3":
                    money_water = m3 * 11.615;
                    break;
                case "Business services":
                case "4":
                    money_water = m3 * 22.068;
                    break;
                default:
                    money_water = 0 ;
                    break;

             }
            return money_water; 
        }
         
        // hàm kiểm tra người nhập có nhập đúng loại khách hàng không 
        static string check_client(string client)
        {
            switch (client)
            {
                case "Household customer":
                case "1":
                    return "Your client code is Household customer!";
                case "Administrative agency":
                case "2":
                case "Public services":
                    return "Your client code is Administrative agency or public services!";
                case "Production units":
                case "3":
                    return "Your client code is Production units!";
                case "Business services":
                case "4":
                    return "Your client code is Business services!";
                default:
                    return "Invalid input!";
            }
        }
    }
}
