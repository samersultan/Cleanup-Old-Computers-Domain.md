## Clean Up Old Computers on Domain Controller 

To get list of all computers with last time accessed

`get-adcomputer -filter * -properties passwordlastset | select name, passwordlastset | sort passwordlastset`

Remove older than 60 days:

    $date = (get-date).adddays(-60)

Then run:


    get-adcomputer -filter {passwordlastset -lt $date} -properties passwordlastset | select name, passwordlastset | sort passwordlastset



And to clean up:

    get-adcomputer -filter {passwordlastset -lt $date} -properties passwordlastset | remove-adobject -recursive -verbose -confirm:$false
    
    
To remove individual computers:

    remove-adcomputer -identity **"computer name here"**





