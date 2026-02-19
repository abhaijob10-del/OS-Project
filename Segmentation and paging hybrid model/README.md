This project is a simulation of the Segmentation with Paging Hybrid Memory Management technique used in Operating Systems. The main aim of this project is to show how a logical address is converted into a physical address using segment table and page table mapping.
The user can enter the segment number, page number, and offset through a simple web interface. Based on the input, the system performs address translation and displays the corresponding physical address. This helps in understanding how segmentation and paging work together in memory management.
The backend logic of this project is implemented using the C programming language and is executed using CGI. The frontend interface is developed using HTML and CSS to provide an interactive simulation.

Technologies Used:
* C Language
* HTML
* CSS
* CGI
* Apache Server
* Ubuntu (WSL)

How to Run
1. Move the compiled CGI file to /usr/lib/cgi-bin/
2. Move the HTML file to /var/www/html/
3. Give execute permission to the CGI file
4. Open http://localhost/ in your browser

Sample Input
Segment Number: 1
Page Number: 2
Offset: 50

The system will generate the corresponding physical address.
