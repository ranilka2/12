using System;
using System.IO;
namespace classes_c_
{
    public class Papper
    {
        private string name;
        private string code;
        private int count;
        public Papper()
        {
            name = "BAG";
            code = "5655";
            count = 0;
        }
        public Papper(string name, string code, int count)
        {
            Name = name;
            Code = code;
            Count = count;
        }


        public int Count
        {
            get { return count; }
            set
            {
                if (value >= 0)
                {
                    count = value;
                }
                else
                {
                    throw new Exception("Can`t be negative value");
                }
            }
        }

        public string Name
        {
            get { return name; }
            set
            {
                if (value != "")
                {
                    name = value;
                }
                else
                {
                    throw new Exception("Can`t be empty Name");
                }
            }
        }
        public string Code
        {
            get { return code; }
            set
            {
                if (value != "")
                {
                    code = value;
                }
                else
                {
                    throw new Exception("Can`t be empty Code");
                }
            }
        }

        public override string ToString() => $"{name} - {code} - {count}";

        public static Papper operator +(Papper prod1, Papper prod2)
        {
            return new Papper(prod1.Name + "/" + prod2.Name, prod1.Code + "/" + prod2.Code, prod1.Count + prod2.Count);
        }

        public static bool operator >(Papper prod1, Papper prod2)
        {
            return prod1.Count > prod2.Count;
        }
        public static bool operator <(Papper prod1, Papper prod2)
        {
            return prod1.Count < prod2.Count;
        }
        public void ToFile()
        {
            using (StreamWriter sw = new StreamWriter("result.txt", true, System.Text.Encoding.Default))
            {
                sw.WriteLine(this.ToString());
                sw?.Close();
            }

        }

    }

    public class Magazine : Papper
    {
        private int energy;
        public int Energy
        {
            get { return energy; }
            set
            {

                if (value >= 0)
                {
                    energy = value;
                }
                else
                {
                    throw new Exception("Can`t be negative value");
                }
            }
        }
        public Magazine() : base()
        {

            Energy = 200;
        }

        public Magazine(string name, string code, int count, int energy) : base(name, code, count)
        {
            Energy = energy;
        }

        public override string ToString()
        {
            return $"{Name} - {Code} -{Energy} - {Count}";
        }

    }

    public class Book : Papper
    {
        public string Color { get; set; }
        public Book() : base()
        {

            Color = "transparent";
        }

        public Book(string name, string code, int count, string color) : base(name, code, count)
        {
            Color = color;
        }

        public override string ToString()
        {
            return $"{Name} - {Code} -{Color} - {Count}";
        }

    }

    public class Newspaper : Papper
    {

        public bool IsToxic { get; set; }
        public  Newspaper() : base()
        {

            IsToxic = true;
        }

        public Newspaper(string name, string code, int count, bool isToxic) : base(name, code, count)
        {
            IsToxic = isToxic;
        }

        public override string ToString()
        {
            return $"{Name} - {Code} -{IsToxic} - {Count}";
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            var products = new Papper[5]{
                new Book(),
                new Newspaper("The Times","Sport",5,false),
                new Magazine("English Football","Food",5,500),
                new Magazine("Fashion","History",10,250),
                new Book("Harry Potter","The Little Prince",6,"Robin Hood")
            };
            foreach (var product in products)
            {
                Console.WriteLine(product);
            }
        }
    }
}
