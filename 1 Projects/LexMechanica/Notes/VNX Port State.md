```perl
sub port_state
{
	my($v) = @_;
	my $ret;
	if(1 == 0) { ; }
	elsif($v eq '0') { $ret = "Ininitialized"; }
	elsif($v eq '1') { $ret = "Unknown"; }
	elsif($v eq '2') { $ret = "Empty"; }
	elsif($v eq '3') { $ret = "Missing"; }
	elsif($v eq '4') { $ret = "Faulted"; }
	elsif($v eq '5') { $ret = "Enabled"; }
	else { $ret = $v; }
	return $ret;
}

sub port_sub_state
{
	my($v) = @_;
	my $ret;
	if(1 == 0) { ; }
	elsif($v eq '0') { $ret = "UNINITIALIZED"; }
	elsif($v eq '1') { $ret = "SFP NOT PRESENT"; }
	elsif($v eq '2') { $ret = "IO NOT PRESENT"; }
	elsif($v eq '3') { $ret = "PORT_NOTPRESNT"; }
	elsif($v eq '4') { $ret = "SFP_MISSING"; }
	elsif($v eq '5') { $ret = "IO_MISSING"; }
	elsif($v eq '6') { $ret = "INCORRECT_SFP"; }
	elsif($v eq '7') { $ret = "IO_INCORRECT"; }
	elsif($v eq '8') { $ret = "SFP_ERROR"; }
	elsif($v eq '9') { $ret = "UNSUPPORTEDSFP"; }
	elsif($v eq '10') { $ret = "IO_ERROR"; }
	elsif($v eq '11') { $ret = "MAXPORTLIMITS"; }
	elsif($v eq '12') { $ret = "IO_POWEROFF"; }
	elsif($v eq '13') { $ret = "UNSUPPORTEDIO"; }
	elsif($v eq '14') { $ret = "GOOD"; }
	elsif($v eq '15') { $ret = "DBERROR"; }
	elsif($v eq '16') { $ret = "SFPFAULTED"; }
	else { $ret = $v; }
	return $ret;
}
```

