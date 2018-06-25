using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace Shift
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }
        string[] arr = { "Nazmul", "Sudipto", "Aniya", "Srijan", "Rajjo", "Valeena", "Rupam", "Ravi", "John", "David", "Denis", "Pinki", "Arpita", "Sangeeta", "Farhan", "Anwarul" };
        // "Sahid", "Saurabh", "Emon", "Mridul", "Mir" };

        int  startIndex = 0;
    

        private void btnShowTextbox_Click(object sender, EventArgs e)
        {
            int NumberOfControls = int.Parse(textBox1.Text);
            int x = 0;
            TextBox tb;
            for (int i = 1; i <= NumberOfControls; i++)
            {
                //creating a control in the run time
                tb = new TextBox();//just to create a text box control inside memory
                tb.Name = "textBox_" + i;
                tb.Location = new Point(x, 0);
                x = x + tb.Width +3;

                panel1.Controls.Add(tb);
            }
         
        }
        private void button1_Click(object sender, EventArgs e)
        {
            //TextBox tb = (TextBox)panel1.Controls.Find("textBox_1",false)[0];
            //tb.Text = "hello";
            int NumberOfControls = int.Parse(textBox1.Text);
            for (int i = 1; i<= NumberOfControls; i++)
            {
                TextBox tb = (TextBox)panel1.Controls.Find("textBox_" + i, false)[0];
                tb.Text = "Hello";
            }
        }
        private void btnSum_Click(object sender, EventArgs e)
        {
            int sum = 0;
            int x;
            int NumberOfControls = int.Parse(textBox1.Text);
            for (int i = 1; i <= panel1.Controls.Count; i++)
            {
                TextBox tb = (TextBox)panel1.Controls.Find("textBox_" + i, false)[0];
                x= int.Parse(tb.Text);
                sum = sum + x;
            }
            MessageBox.Show(sum.ToString());
        }

        private void btnShiftToRight_Click(object sender, EventArgs e)
        {
           
            int NumberOfControls = int.Parse(textBox1.Text);

            TextBox tbLast = (TextBox)panel1.Controls.Find("textBox_" + NumberOfControls, false)[0];
            string lastValue = tbLast.Text;

            for (int i = NumberOfControls - 1; i >= 1; i--)
            {
                TextBox tb = (TextBox)panel1.Controls.Find("textBox_" + i, false)[0];
                TextBox tbNext = (TextBox)panel1.Controls.Find("textBox_" + (i + 1), false)[0];
                tbNext.Text = tb.Text;
            }
            TextBox tbFirst = (TextBox)panel1.Controls.Find("textBox_" + 1, false)[0];
            tbFirst.Text = lastValue;




        }

        private void btnLeftShift_Click(object sender, EventArgs e)
        {
            listBox1.Items.Clear();
           

            //print next 5 data starting from startIndex
            int NumberOfControls = int.Parse(textBox1.Text);
            int NameCount = 0;

            if (NumberOfControls > arr.Length)
                NumberOfControls = arr.Length;


            int NumberOfElementsToChoose = NumberOfControls;


            if (arr.Length - startIndex < NumberOfControls)
            {
                NumberOfElementsToChoose = arr.Length - startIndex;
            }
            int lastValidIndex = startIndex + (NumberOfElementsToChoose - 1);

            for (int i = startIndex; i <= lastValidIndex; i++)
            {
                NameCount++;
               // MessageBox.Show(NameCount+" "+arr[i]);
                TextBox tb = (TextBox)panel1.Controls.Find("textBox_" + NameCount, false)[0];
                tb.Text = arr[i];

                listBox1.Items.Add(arr[i]);
            }
            if (arr.Length - startIndex < NumberOfControls)
            {
                int missingCount = (NumberOfControls - (arr.Length - startIndex));
                //MessageBox.Show("Incomplete with " + missingCount);
                for (int i = 0; i <= missingCount - 1; i++)
                {
                    NameCount++;
                    //    MessageBox.Show(NameCount+" "+ arr[i]);
                    TextBox tb = (TextBox)panel1.Controls.Find("textBox_" + NameCount, false)[0];
                    tb.Text = arr[i];

                    listBox1.Items.Add(arr[i]);
                }
               
            }
            startIndex++;
            if (startIndex == arr.Length)
                startIndex = 0;



        }
    }
}
